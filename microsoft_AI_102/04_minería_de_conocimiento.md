# Implementación de minería de conocimiento con Azure AI Search

> **💡 Concepto clave ➜ Azure AI Search**: Servicio en la nube para **indexar** y **buscar** datos de múltiples fuentes.

**Azure AI Search** permite organizar información masiva (documentos, bases de datos, etc.) en un **índice de búsqueda** optimizado. Cada solución incluye varios componentes (origenes de datos, **aptitudes cognitivas**, **indexadores**, y **índices**) que trabajan juntos para extraer y enriquecer datos con IA. Por ejemplo, se pueden usar aptitudes predefinidas (detección de idioma, frases clave, sentimiento, entidades, OCR de imágenes…) para enriquecer los datos de origen. Luego un **indexador** ejecuta estas aptitudes, mapea los resultados a un **índice** y hace que los datos sean consultables. El índice final es una colección de documentos JSON, donde cada campo tiene atributos como *searchable*, *filterable*, *sortable*, etc. El resultado es una búsqueda completa y relevante a gran escala.

* 🗂️ **Origen de datos**: puede ser Azure Blob, SQL Database, Cosmos DB, etc. Los datos se extraen para indexarlos.
* 🤖 **Aptitudes cognitivas**: transforman datos de origen en insights (idioma, *keyphrases*, sentimiento, entidades, texto de imágenes…). Se agrupan en un **conjunto de aptitudes** (skillset) y cada aptitud puede ser predefinida o **personalizada**.
* 🏎️ **Indexer**: motor que aplica el conjunto de aptitudes a cada documento y alimenta los resultados al índice. Se puede programar periódicamente.
* 📑 **Índice**: almacena los documentos enriquecidos. Cada campo en el índice puede ser *key* (ID único), *searchable* (texto buscable), *filterable*, *sortable*, *facetable*, *retrievable*. Las consultas y filtros se aplican sobre estos campos.

**Autoevaluación**:

1. ¿Qué es Azure AI Search y para qué se usa?
2. Nombra tres componentes clave de una solución de búsqueda.
3. ¿Cuál es la diferencia entre un indexador y un índice?


<br><br><br>
## Creación de una solución de Azure AI Search

> **💡 Concepto clave ➜ Solución de búsqueda básica**: Crear un recurso *Azure AI Search*, elegir un plan (Free/Básico/Estándar/Large), y configurar réplicas y particiones según escalabilidad.

Para iniciar, primero **creamos un servicio de búsqueda** en Azure. Al crearlo, elegimos un *plan de tarifa* (gratuito, básico o estándar) que define cuántos índices, almacenamiento y características tenemos. Luego ajustamos la escalabilidad con **réplicas** (manejan concurrencia de consultas) y **particiones** (dividen índices grandes). El número de *unidades de búsqueda* es réplicas × particiones. *¡Importante!* el nivel de servicio no se puede cambiar después, así que elige bien.

A continuación, definimos un **esquema de índice** donde listamos los campos (nombre, tipo, atributos). Por ejemplo, un índice de hoteles podría tener campos *HotelId* (key), *HotelName*, *Category*, *Tags*, *Description*. Luego cargamos los datos al índice: esto puede hacerse con un indexador (que extrae de un origen existente) o insertando documentos directamente.

**Ejemplo de creación de índice (Python)** usando la biblioteca `azure-search-documents`:

```python
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import SearchIndex, SimpleField, SearchableField
from azure.core.credentials import AzureKeyCredential

client = SearchIndexClient(endpoint, AzureKeyCredential(api_key))
fields = [
    SimpleField(name="HotelId", type="Edm.String", key=True),
    SearchableField(name="Description", type="Edm.String")
]
index = SearchIndex(name="hotels", fields=fields)
client.create_index(index)
```

**Ejemplo con REST (curl)**:

```bash
curl -X PUT "https://<servicio>.search.windows.net/indexes/hotels?api-version=2023-07-01"
 -H "Content-Type: application/json" -H "api-key: <admin-key>" -d '{
   "name": "hotels",
   "fields": [
     {"name":"HotelId","type":"Edm.String","key":true},
     {"name":"Description","type":"Edm.String","searchable":true}
   ]
 }'
```



**Autoevaluación**:

1. ¿Qué factores definen una “unidad de búsqueda” en Azure Search? (Piensa en réplicas y particiones)
2. ¿Qué atributos comunes puede tener un campo de índice? Menciona al menos tres.
3. ¿Qué implica elegir un plan de tarifa de Azure Search?


<br><br><br>
## Búsqueda en el índice

> **💡 Concepto clave ➜ Consultas en Azure Search**: Se consulta el índice vía REST o SDK, usando operadores como *search*, *filter*, *orderby*; se pueden **mejorar resultados** con scoring profiles, synonym maps o búsquedas semánticas.

Con el índice creado y documentos cargados, los clientes pueden realizar **consultas**. Por ejemplo, buscando el término *luxury* en todos los campos:

```
GET https://<servicio>.search.windows.net/indexes/hotels/docs?search=luxury&$select=HotelId,HotelName&api-version=2023-07-01
```

También se pueden aplicar filtros (`$filter`), ordenar (`$orderby`) y paginar (`$top`, `$skip`).

* 💬 **Sintaxis Lucene**: Se pueden usar *queryType=full* para expresiones complejas (prefijos, rangos, operadores booleanos). Además, **priorizar términos** es posible con boost, por ejemplo `"hotel^3 luxury"` para que “hotel” pese más en la puntuación.
* 🎯 **Scoring Profiles**: Definen pesos de campos y funciones de boosting basados en campos numéricos o frescura. Por ejemplo, un perfil puede hacer que *Description* valga 5 veces más que *Category*. En JSON de índice: `"scoringProfiles": [ { "name": "perfil1", "text": {"weights":{"Description":5, "Category":2}} } ]`.
* 🌀 **Filtros y orden**: Se pueden filtrar por campos (p.ej. `Category eq 'Luxury'`) y ordenar resultados, incluso por **distancia geográfica** usando funciones `geo.distance`. Los campos de ubicación deben ser tipo `Edm.GeographyPoint`.
* 🧭 **Búsqueda semántica (L2)**: Habilite una configuración semántica en el índice y use `queryType=semantic` para obtener resultados con relevancia mejorada y respuestas (“captions”) en lenguaje natural.

**Ejemplo de consulta REST (curl)**:

```bash
curl -X GET "https://<servicio>.search.windows.net/indexes/hotels/docs?search=luxury&$count=true&api-version=2023-07-01" \
 -H "api-key: <query-key>"
```

**Ejemplo (Python)** usando SDK:

```python
from azure.search.documents import SearchClient
client = SearchClient(endpoint, "hotels", AzureKeyCredential(query_key))
results = client.search(search_text="luxury", select=["HotelName","Category"])
for r in results:
    print(r["HotelName"], "-", r["Category"])
```

**Autoevaluación**:

1. ¿Cómo se ajusta la relevancia de resultados con un *scoring profile*?
2. ¿Cuál es la diferencia entre consulta simple (por defecto) y Lucene (full)?
3. ¿Cómo ordenarías resultados por proximidad a una ubicación? (menciona función geoespacial).


<br><br><br>
## Capacidades personalizadas (Custom Skills)

> **💡 Concepto clave ➜ Aptitudes personalizadas**: Funciones externas (p.ej. Azure Functions) que extienden el enriquecimiento con lógica propia (p.ej. IA de clasificación, visión, ML).

Las **aptitudes integradas** cubren muchos escenarios, pero a veces necesitamos lógica específica. Las **aptitudes personalizadas** permiten llamar a cualquier servicio web durante la indexación. Por ejemplo, podríamos usar un modelo de *Azure Cognitive Services - Language* para clasificar texto, o un servicio de *Azure Machine Learning* para predecir campos. Técnicamente, creamos un servicio web (normalmente una *Azure Function* o API) que cumple con el **esquema JSON** de habilidades de Azure Search.

* 📐 **Esquema de Skills**: Los endpoints deben recibir y devolver JSON con array `values[{recordId, data: {...}}]`. Azure exige este formato para entradas y salidas de cada documento.
* 🔧 **Integración en Skillset**: En el `skillset` JSON, se agrega un objeto con `"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill"`. Se indican la `uri` (URL de la función), encabezados, `context` (parte del documento donde aplicar) y mapeos de `inputs` → campos de índice y `outputs` → nuevos campos. Ejemplo:

  ```json
  "skills": [
    {
      "@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
      "uri": "https://<mi-funcion>.azurewebsites.net/api/miskill",
      "inputs": [{ "name": "text", "source": "/document/Content" }],
      "outputs": [{ "name": "categories", "targetName": "DetectedCategories" }]
    }
  ]
  ```
* 🧠 **Clasificación de texto personalizada**: Con Azure Language Studio, entrenas un modelo de *multi-clase* o *multi-etiqueta* (según si cada doc tiene una o varias categorías). Después implementas el modelo (p.ej. como Function) y lo usas en una skill. Esto enriquece el índice con campos categorizados.
* 📊 **Aptitud AML**: Existe un tipo especial `AmlSkill`. En el skillset se define con `"@odata.type": "#Microsoft.Skills.Custom.AmlSkill"`, incluyendo la URL del endpoint de un modelo en Azure ML y la clave de acceso. Mapas sus entradas (`inputs`) y salidas (`outputs`) a campos del documento.

**Autoevaluación**:

1. ¿Qué formato JSON debe seguir una aptitud personalizada? Describe brevemente.
2. ¿En qué casos usarías una clasificación *multiclase* vs *multi-etiqueta*?
3. ¿Cómo especificas un `WebApiSkill` en el JSON de un skillset?


<br><br><br>
## Almacén de conocimiento

> **💡 Concepto clave ➜ Almacén de conocimiento**: Destino (Blob, tablas, archivos) donde se guardan los datos enriquecidos fuera del índice.

Más allá del índice, es útil **guardar** los resultados de enriquecimiento para análisis independientes. El **almacén de conocimiento** almacena **proyecciones** de los datos enriquecidos: pueden ser objetos JSON, tablas relacionales o archivos (p.ej. imágenes extraídas). Para configurarlo se añade un bloque `knowledgeStore` al skillset:

* 📊 **Proyecciones de objeto**: Guarda documentos JSON. Se crea un contenedor en Azure Blob donde se vuelcan cada registro enriquecido.
* 📋 **Proyecciones de tabla**: Genera tablas de Azure Storage. Cada tabla tiene una clave única (`generatedKeyName`) y columnas basadas en los campos del skillset. Ideal para reportes y BI.
* 📁 **Proyecciones de archivo**: Guarda archivos como imágenes extraídas (por ejemplo, OCR). Se configuran apuntando a un contenedor.

Ejemplo (fragmento JSON):

```json
"knowledgeStore": {
  "storageConnectionString": "<cadena de Storage>",
  "projections": [
    {
      "objects": [ { "storageContainer": "contenido", "source": "/projection" } ],
      "tables":   [ { "tableName": "docs", "generatedKeyName": "doc_id", "source": "/projection" } ],
      "files":    [ { "storageContainer": "imagenes", "source": "/document/normalized_images/*" } ]
    }
  ]
}
```


En este caso se guardan los campos combinados (usando por ejemplo un *ShaperSkill*) en un campo `/projection`, que se vuelca como objeto JSON y fila de tabla. Azure creará contenedores/tablas según sea necesario.

**Autoevaluación**:

1. ¿Qué ventajas tiene usar un almacén de conocimiento? Menciona dos ejemplos de uso.
2. ¿Qué es una *proyección* en este contexto?
3. ¿Cómo configuras una proyección de tabla en el skillset? (Explica brevemente).


<br><br><br>
## Características avanzadas de búsqueda

> **💡 Concepto clave ➜ Búsqueda avanzada**: Configurar relevancia y análisis según necesidades; incluye *scoring*, *analizadores*, *sinónimos*, *idiomas* y funciones geo.

Además de lo básico, Azure Search ofrece varias mejoras clave:

* 🎯 **Prioridad de términos (Boosting)**: Al escribir consultas, se puede aumentar la importancia de ciertas palabras (ej. `hotel^3` da más peso al término “hotel”).
* 📈 **Perfiles de puntuación**: Como vimos antes, ponderan campos o usan funciones (distancia, fecha) para ajustar la ordenación de resultados.
* 🔤 **Analizadores y tokenización**: Por defecto se usa el analizador Lucene genérico. Para campos específicos se pueden usar *analizadores de idioma* (p.ej. `"analyzer": "es.microsoft"`) o crear **analizadores personalizados** combinando filtros de caracteres, tokenizadores y filtros de tokens. Esto permite, por ejemplo, usar una expresión regular o manejar casos de uso especiales (códigos postales, NLP de idiomas específicos).
* 🌐 **Búsqueda multilingüe**: Se pueden añadir varios campos (p.ej. `description`, `description_fr`, `description_de`) cada uno con el analizador de idioma correspondiente. Luego en la aplicación se consulta según el idioma del usuario. También es posible usar Cognitive Services para traducir texto en pipeline y llenar esos campos.
* 📍 **Geo-búsqueda**: Con campos tipo `Edm.GeographyPoint`, Azure Search permite filtrar por distancia (`$filter=geo.distance(Location, POINT) le R`) y ordenar por proximidad (`$orderby=geo.distance(Location, POINT) asc`). También dispone de `geo.intersects` para polígonos.

**Autoevaluación**:

1. Da un ejemplo de cuándo usarías un analizador de idioma específico en un campo.
2. ¿Qué efecto tiene ordenar por `geo.distance` en los resultados?
3. Explica brevemente cómo la búsqueda semántica mejora la relevancia (no olvides *L2 classification*).


<br><br><br>
## Ingesta con Azure Data Factory y API Push

> **💡 Concepto clave ➜ Ingesta de datos externos**: Además de indexadores, Azure Data Factory (ADF) o la API REST permiten **insertar datos** en el índice desde cualquier origen.

Para datos fuera de Azure o en formatos especiales, se usan métodos de inserción manuales:

* 🏗️ **Azure Data Factory**: Puedes crear una *pipeline* en ADF con actividad de copia. Se conecta a casi cualquier fuente (bases de datos, HTTP, etc.) y usa el conector de **Azure Search** como *sink*. Pasos básicos: crear índice, en ADF definir un *dataset* de origen, un *dataset* del tipo Azure Search, y mapear campos. Al ejecutar la pipeline, se envían lotes de documentos al índice. Este enfoque “sin código” es ideal cuando trabajas con datos heterogéneos.
* 🚀 **API REST de inserción**: Permite cargar directamente documentos vía HTTP. Se hace una llamada `POST https://<servicio>.search.windows.net/indexes/<index>/docs/index?api-version=...` con el body JSON que indique las acciones (`upload`, `merge`, etc.). Ejemplo de cuerpo:

  ```json
  {
    "value": [
      {
        "@search.action": "upload",
        "id": "123",
        "firstName": "Ana",
        "lastName": "García",
        ...
      }
    ]
  }
  ```

  Azure recomienda enviar hasta 1000 documentos por lote (o 16 MB) para mejor rendimiento.

**Autoevaluación**:

1. ¿Cuándo usarías Azure Data Factory en lugar de un indexador para cargar datos?
2. En la API REST de inserción, ¿qué significa la acción `"@search.action": "mergeOrUpload"`?
3. ¿Qué credencial necesitas para usar la API de inserción de documentos? (admin key o query key?)


<br><br><br>
## Mantenimiento: seguridad, rendimiento y costos

> **💡 Concepto clave ➜ Mantenimiento de solución**: Proteger datos con cifrado y redes, escalar réplicas/particiones para rendimiento, controlar costos con niveles adecuados y supervisar con Azure Monitor.

Para asegurar **seguridad** y **rendimiento**, y controlar **costos**, se siguen buenas prácticas:

* 🔒 **Seguridad**:

  * **Cifrado**: Todos los datos en reposo se cifran por defecto con claves de servicio. Para mayor control, puedes usar tus propias claves en Azure Key Vault (doble cifrado).
  * **Red**: Restringe el acceso al endpoint público con **firewall de IP** o habilita un **endpoint privado/VNet** si solo se usa internamente. Para indexadores, asegúrate de que las fuentes (bases de datos, blobs) también estén protegidas (credenciales seguras).
  * **Acceso**: Separa roles de lectura/escritura usando *admin keys* vs *query keys* o Azure AD. A nivel de documento, implementa filtros o seguridad en la capa de aplicación (Azure Search no tiene control por usuario integrado).

* ⚡ **Rendimiento**:

  * Ajusta réplicas/particiones: más réplicas aumentan throughput de consultas; más particiones soportan índices grandes y throughput de escritura.
  * Monitorea métricas de Azure Monitor (Search QPS, latencia, throttling). Habilita *diagnóstico* a Log Analytics para análizar cuellos de botella. Si ves códigos 503 (throttle) o 207 (indexación lenta), escala recursos o optimiza consultas.
  * Escribe consultas eficientes: limita campos con `$select`, evita wildcard excesivos y perfiles de puntuación complejos si no son necesarios.

* 💰 **Costos**:

  * Usa la **calculadora de Azure** para estimar costos según nivel y unidades de búsqueda. Un servicio S2 con 4 unidades, por ejemplo, tiene costo mensual = (precio unidad × 4) + extras (búsqueda semántica, AI de visión, etc.).
  * Optimiza el nivel: no sobredimensionar réplicas/particiones. En entornos de desarrollo usa el nivel gratuito o Básico, y sube a Standard solo en producción.
  * Controla costos en **Azure Cost Management** con presupuestos/alertas para evitar sobreconsumo.

**Autoevaluación**:

1. ¿Qué debes hacer si observas muchos errores 503 en los logs de búsqueda?
2. ¿Cuál es el beneficio de tener réplicas en diferentes zonas de disponibilidad?
3. Menciona dos métricas útiles que podrías graficar en Azure Monitor para Search.


<br><br><br>
## Confiabilidad y disponibilidad

> **💡 Concepto clave ➜ Alta disponibilidad**: Aumentar réplicas y usar zonas/regiones para evitar fallos. Replicar datos y enrutar usuarios globalmente.

Para que la búsqueda esté siempre activa:

* 🛡️ **Réplicas múltiples**: Se requieren ≥2 réplicas para tolerancia a fallos. Garantiza \~99.9% consultas; ≥3 réplicas cubren también la indexación.
* 🌐 **Availability Zones**: Aloja réplicas en zonas distintas para resistencia a caída regional (solo en niveles Standard+).
* 🌎 **Distribución geográfica**: Crea servicios de búsqueda en distintas regiones si usuarios/negocio lo requieren. Sin conmutación automática, deberás replicar índices manualmente (ej. pipelines o API push) y usar Azure Traffic Manager para enrutar consultas al servicio más cercano. Esto mejora latencias y tolerancia a desastres.

Azure no provee respaldo automático del índice, así que es buena práctica exportar los datos clave (p.ej. documentos originales) para reindexar en caso de falla mayor.

**Autoevaluación**:

1. ¿Qué implica perder una zona de disponibilidad si tienes una sola réplica?
2. ¿Cómo manejarías una falla total en una región?
3. ¿Qué porcentaje de SLA ofrece Azure Search con 3 réplicas?


<br><br><br>
## Supervisión y diagnóstico

> **💡 Concepto clave ➜ Monitorización**: Usar Azure Monitor y Search Diagnostic Logs para medir latencia, consultas por segundo y tasas de aciertos/errores. Crear alertas según métricas clave.

Para mantener la salud:

* 📊 **Azure Portal**: En la vista de *Supervisión* del servicio se ven métricas básicas: *Search Queries per Second*, *Avg Latency*, *Throttled Queries %*. En *Uso* aparece CPU, memoria, etc.
* 📈 **Azure Monitor y Log Analytics**: Habilita diagnostic logs (AzureDiagnostics, AzureMetrics). Esto permite consultas y gráficos personalizados. Algunas métricas clave: `SearchLatency`, `SearchQueriesPerSecond`, `ThrottledSearchQueriesPercentage`, `DocumentsProcessedCount`. Por ejemplo, trazar latencia vs porcentaje de queries limitadas revela si el servicio sufre de throttling.
* 🔔 **Alertas**: Define alertas en Azure Monitor para umbrales como *latencia alta* o *errores de indexador* para acción inmediata.
* 🔍 **Debug en Portal**: Usa la herramienta **Sesión de depuración** integrada para inspeccionar pipelines de indexación. Permite rastrear un documento a través de cada aptitud, ver errores y probar soluciones.

**Autoevaluación**:

1. ¿Qué información te da la métrica `SearchQueriesPerSecond`?
2. ¿Qué pasos seguirías si encuentras un error en un indexador?
3. ¿Cómo habilitas la recolección de logs detallados para Azure Search?


<br><br><br>
## Clasificación semántica (L2)

> **💡 Concepto clave ➜ Búsqueda semántica**: Utiliza IA de lenguaje natural para mejorar la relevancia más allá de palabras clave, extrayendo respuestas o resúmenes de cada resultado.

La **clasificación semántica** aplica aprendizaje profundo (nivel L2) en consultas en texto libre. No nos quedamos en coincidencias literales, sino que entendemos contexto y proporcionamos fragmentos relevantes (respuestas) extraídos de los documentos. Para habilitarla:

* Se habilita **semantic ranking** en el índice (en portal o JSON) definiendo un *configuration* con campos prioritarios.
* En la consulta REST o SDK, usar `queryType=semantic` y `"queryAnswer": "extractive"` para recibir respuestas. Por ejemplo:

  ```json
  POST /indexes/myindex/docs/search?api-version=2023-07-01-Preview
  { "queryType": "semantic", "query": "¿Cuál es el mejor hotel cerca de París?", "top": 3 }
  ```

  El resultado incluirá los documentos más relevantes y, opcionalmente, una respuesta generada.

La semántica **aumenta la precisión** al entender sinónimos y contexto. Por ejemplo, si el usuario pregunta “¿qué hoteles de lujo hay?”, la búsqueda semántica promovará resultados cuyo contenido indica prestigio, incluso si la palabra exacta “lujo” no aparece.

**Autoevaluación**:

1. ¿Qué parámetros cambias en una consulta para activarle la semántica?
2. ¿Qué hace la respuesta extractiva en la consulta semántica?
3. ¿Por qué es útil habilitar `semanticConfiguration` en el índice?


<br><br><br>
## Búsqueda vectorial

> **💡 Concepto clave ➜ Búsqueda vectorial**: Encuentra documentos relacionados usando vectores numéricos (embeddings) en lugar de solo texto; ideal para similitud semántica.

La **búsqueda vectorial** permite consultar no sólo con palabras, sino con representaciones vectoriales de contenido (texto, imágenes, etc.). Para usarla:

* 📐 **Índice**: Debe incluir un campo de vectores, por ejemplo: `"name": "imageVector", "type": "Collection(Edm.Single)", "dimensions":1536`. Este campo almacenará el embedding (generado por Cognitive Search o externamente) de cada documento.
* 🛠️ **Inserción**: Al indexar documentos, incluimos el vector en el campo correspondiente. Se pueden usar las aptitudes integradas de **Embeddings de Azure AI** que llaman a modelos de OpenAI para generar vectores a partir de texto/imagen.
* 🔍 **Consulta**: La llamada REST a `/docs/search` lleva un objeto `vector`, indicando el campo y el vector de la consulta, por ejemplo:

  ```json
  {
    "vector": {
      "fields": "contentVector",
      "value": [0.123, -0.456, ...], 
      "k": 5
    }
  }
  ```

  Esto devuelve los *k* documentos cuyos vectores sean más cercanos (por similitud coseno). Azure Search también soporta filtros adicionales junto al vector query.

La búsqueda vectorial **detecta similitud conceptual**; por ejemplo, consultando por un fragmento de texto, se encuentran documentos relacionados incluso sin compartir palabras exactas.

**Autoevaluación**:

1. ¿Cómo debes definir un campo de vectores en el índice? Nombra un atributo clave.
2. ¿Qué representa la consulta `k` en la operación vectorial?
3. ¿Por qué podríamos querer usar vectores en lugar de búsqueda por palabras clave?


<br><br><br>
## Glosario

* **Azure AI Search**: Servicio de búsqueda basado en la nube de Microsoft para indexar y consultar datos de múltiples orígenes.
* **Índice de búsqueda**: Estructura que almacena documentos JSON con campos configurados (*searchable*, *filterable*, *sortable*, etc.).
* **Indexador**: Motor que extrae datos del origen, aplica aptitudes cognitivas y almacena los resultados en el índice.
* **Aptitud (Skill)**: Módulo que procesa datos (predefinido o personalizado) durante la indexación, generando nuevos insights (texto, imágenes, etc.).
* **Conjunto de aptitudes (Skillset)**: Agrupación de aptitudes que define la canalización de enriquecimiento.
* **Almacén de conocimiento**: Destino externo (Blob Storage, tablas) donde se guardan copias de los datos enriquecidos generados por el skillset.
* **ShaperSkill**: Aptitud integrada que consolida campos en estructuras JSON simples para facilitar proyecciones.
* **Perfil de puntuación (Scoring Profile)**: Configuración de campo de índice que pondera automáticamente campos o aplica funciones (frescura, distancia) para modificar la relevancia.
* **Analizador (Analyzer)**: Componente que divide texto en tokens (palabras). Puede ser *predeterminado*, específico de idioma o **personalizado** (combinando filtros/tokenizadores).
* **Clasificación multiclase**: Modelo de IA que asigna un documento a una sola categoría (una etiqueta).
* **Clasificación multi-etiqueta**: Modelo que asigna varias categorías posibles a un mismo documento.
* **Consulta semántica**: Query con `queryType=semantic` que usa NLP para entender contexto y devuelve respuestas en lenguaje natural.
* **Búsqueda vectorial**: Técnica de IR que usa vectores numéricos (embeddings) de documentos/consultas para encontrar similitudes más allá de palabras clave.
* **Unidad de búsqueda (Search Unit)**: Medida de capacidad de Azure Search (una réplica × una partición). A mayor SU, más escala y rendimiento.


<br><br><br>
## Resumen (Tarjetas de memoria)

| **Sección**                                       | **A memorizar (Idea clave)**                                                                                         |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| 1. Creación de solución de Azure AI Search        | Configurar servicio de Search con plan adecuado, réplicas y particiones. Definir índices y cargar datos.             |
| 2. Búsqueda en el índice                          | Realizar consultas REST/SDK, usar `$filter`, `$orderby`, boosting de términos y scoring profiles para relevancia.    |
| 3. Aptitudes personalizadas                       | Integrar IA propia (Azure Functions/ML) en la canalización con `WebApiSkill` o `AmlSkill`.                           |
| 4. Almacén de conocimiento                        | Guardar datos enriquecidos fuera del índice en Azure Storage o tablas, usando proyecciones definidas en el skillset. |
| 5. Búsqueda avanzada                              | Mejorar relevancia usando perfiles de puntuación, analizadores personalizados, campos multilingües y funciones geo.  |
| 6. Ingesta de datos externos                      | Usar Azure Data Factory o la API REST (`docs/index`) para insertar documentos en el índice desde cualquier origen.   |
| 7. Mantenimiento (seguridad, rendimiento, costos) | Asegurar con cifrado/redes, escalar réplicas/particiones según demanda, y controlar gastos con niveles adecuados.    |
| 8. Confiabilidad y alta disponibilidad            | Añadir réplicas (>=2) y zonas, replicar servicios en varias regiones para tolerancia a fallos.                       |
| 9. Monitorización y diagnóstico                   | Usar Azure Monitor/Log Analytics para métricas de latencia y QPS; debug con sesiones de depuración en Portal.        |
| 10. Búsqueda semántica                            | Habilitar semantic ranking (L2) para mejorar relevancia y obtener respuestas generadas en lenguaje natural.          |
| 11. Búsqueda vectorial                            | Incorporar campos vectoriales (embeddings) y usar consultas KNN para similitud semántica entre documentos.           |


<br><br><br>
## Tabla de atajos (cheat-sheet)

| **Servicio / Acción**              | **Python (SDK)**                                                                                                                                                                                                                                            | **REST (curl)**                                                                                                                                                                                                                                                                   |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Crear índice** (Azure AI Search) | `SearchIndexClient(endpoint, AzureKeyCredential(key)).create_index(SearchIndex(...))`                                                                                                                                                                       | `curl -X PUT "https://<servicio>.search.windows.net/indexes/miindice?api-version=2023-07-01" -H "api-key: <admin>" -H "Content-Type: application/json" -d '{...schema...}'`                                                                                                       |
| **Cargar documentos**              | `SearchClient(...).upload_documents([{"id": "1", "campo": "valor", ...}])`                                                                                                                                                                                  | `curl -X POST "https://<servicio>.search.windows.net/indexes/miindice/docs/index?api-version=2023-07-01" -H "api-key: <admin>" -H "Content-Type: application/json" -d '{"value":[{"@search.action":"upload","id":"1","campo":"valor"}]}'`                                         |
| **Consulta de búsqueda**           | `SearchClient(...).search("término", select=["campos"], filter="campo eq 'x'")`                                                                                                                                                                             | `curl -X GET "https://<servicio>.search.windows.net/indexes/miindice/docs?search=texto&$filter=campo eq 'x'&api-version=2023-07-01" -H "api-key: <query>"`                                                                                                                        |
| **Scoring profile** (definición)   | N/A (se configura en el JSON de índice)                                                                                                                                                                                                                     | Incluir `"scoringProfiles": [{"name":"perf","text":{"weights":{"campo":2}}}]` en el esquema del índice.                                                                                                                                                                           |
| **Aptitud personalizada**          | N/A (configuración en skillset JSON)                                                                                                                                                                                                                        | Incluir en `skillset`: `{"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill", "uri": "<URL>", "inputs":[...], "outputs":[...]}`.                                                                                                                                                |
| **Clasificación de texto**         | Usar `TextAnalyticsClient` de Azure AI Language: <br>`python<br>client = TextAnalyticsClient(endpoint, AzureKeyCredential(key))<br>doc = [{"id":"1","text":"..."}]<br>res = client.begin_multi_label_classify(doc, project_name, deployment_name).result()` | `curl -X POST "https://<endpoint>/language/analyze-text?api-version=2022-05-01" -H "Ocp-Apim-Subscription-Key: <key>" -d '{"kind":"SingleLabelClassify","analysisInput":{"documents":[{"id":"1","text":"..."}]},"parameters":{"projectName":"<proj>","deploymentName":"<dep>"}}'` |
| **Crear canalización ADF**         | `az datafactory pipeline create -g RG -n MiADF -f MiFactory -p '{"properties":{...}}'` (Azure CLI)                                                                                                                                                          | No aplica (configuración visual en Azure Data Factory).                                                                                                                                                                                                                           |

*Nota:* Algunos servicios (p.ej. Azure Data Factory) se configuran principalmente via portal o CLI, por lo que los atajos se refieren a opciones disponibles (por ejemplo, Azure CLI para ADF). La **Azure Data Factory** en Python se manejaría con `azure-mgmt-datafactory` (no mostrado aquí por brevedad).
