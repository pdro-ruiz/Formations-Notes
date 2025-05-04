# Document Intelligence

> **Concepto clave ➜** *Azure AI Document Intelligence* es un servicio de Azure que extrae datos estructurados de formularios escaneados o PDFs.

Los *formularios* físicos o digitales pueden procesarse automáticamente, ahorrando tiempo y evitando errores manuales. Por ejemplo, una empresa de encuestas con entradas de datos manuales costosas puede usar Document Intelligence para extraer automáticamente nombres, teléfonos, respuestas, etc. y guardar los resultados en una base de datos. Para diseñar una solución robusta, es clave entender sus **componentes**: modelos (precompilados o personalizados), API (puntos de conexión), y herramientas (Portal, Studio) que se adapten a los formularios de la empresa. Además, se debe aplicar **IA responsable**: seguir principios como **equidad, fiabilidad, privacidad, inclusión, transparencia y responsabilidad** al validar resultados, limitar datos y mantener supervisión humana.

**Preguntas de auto-test:**

* ¿Qué es Azure AI Document Intelligence y qué ventajas ofrece frente al ingreso manual de datos?
* ¿Cuáles son dos principios éticos clave al implementar una solución de IA?
* ¿Qué componentes (recursos y herramientas) se necesitan conocer para integrar Document Intelligence en una aplicación?

<br><br><br>
## Uso de modelos en Document Intelligence

> **Concepto clave ➜** Un *modelo* en Document Intelligence describe la estructura del formulario esperado, mejorando la precisión de la extracción de datos.

Document Intelligence genera resultados en **JSON**, compatible con bases de datos y lenguajes de programación. Incluye varios **modelos precompilados** listos para tipos comunes de documentos. Por ejemplo:

* 🔍 **Lectura (Read).** Extrae *texto plano*: palabras, líneas y detecta idioma en documentos impresos o manuscritos.
* 📄 **Documento general.** Extrae *pares clave–valor* y *tablas* de un documento sin entrenamiento adicional.
* 🖼 **Diseño (Layout).** Extrae texto y **estructura** de formularios, incluyendo marcas de selección (casillas, radio buttons).

También hay modelos predefinidos para documentos específicos: factura, recibo, W-2 (EE. UU.), identificación, tarjeta de presentación, etc. Por ejemplo, el modelo **Factura** extrae campos típicos como cliente, fechas, totales y cada línea de ítems; el modelo **Recibo** extrae comerciante, totales, impuestos, hora y líneas de productos.

> ❗ **Diferencia clave:** Document Intelligence vs. Azure AI Vision. El servicio *Vision OCR* solo lee texto plano de imágenes. En cambio, Document Intelligence realiza un análisis **más sofisticado**: identifica texto estructurado, pares clave-valor, tablas y campos específicos. Use Vision OCR (u otro OCR básico) solo si necesita extraer texto sin contexto. Para soluciones completas de análisis de formularios, Document Intelligence es más adecuado.

Si los formularios tienen un formato único, puede **crear un modelo personalizado**: se entrena con ejemplos de formularios etiquetados para extraer exactamente los campos deseados. Además, puede combinar varios modelos personalizados en un **modelo compuesto**, de modo que el servicio elija automáticamente el modelo adecuado según el tipo de documento (el resultado JSON incluye un campo `docType` que indica cuál se usó).

**Preguntas de auto-test:**

* ¿Cuál es la función de un modelo en Document Intelligence?
* Mencione tres modelos precompilados generales y qué extraen.
* ¿En qué se diferencia el análisis de Document Intelligence del OCR simple de Vision?
* ¿Qué hace un modelo compuesto en Azure AI Document Intelligence?

<br><br><br>
## Planificación y recursos de Azure AI Document Intelligence

> **Concepto clave ➜** Un *recurso de Azure AI Document Intelligence* provee el *punto de conexión* (endpoint) y la *clave de acceso* (key) necesarios para autenticar llamadas al servicio.

Para usar Document Intelligence, primero cree un recurso en su suscripción de Azure. En el portal de Azure, seleccione **Crear recurso** → *Documento de inteligencia (Azure AI)*. Elija suscripción, grupo de recursos, ubicación y nombre. Luego seleccione un *nivel de tarifa* (p. ej. Gratis F0 o Estándar S0).

* 📌 *Nota:* El nivel Gratis F0 tiene límites bajos y no está disponible para recursos multisitio. El nivel Estándar S0 permite más transacciones y puede ampliarse (vía soporte) si hay cupos insuficientes.

Al crear el recurso, Azure asigna un **endpoint** (URL) y una **clave** única. La *conexión* se realiza incluyendo este endpoint en el cliente y la clave en las cabeceras (por ejemplo, `Ocp-Apim-Subscription-Key`). En el portal, en **Claves y puntos de conexión** del recurso, copie la “Clave 1” (o 2) y el endpoint. En su código deberá usarlos así:

```python
from azure.core.credentials import AzureKeyCredential
from azure.ai.documentintelligence import DocumentIntelligenceClient

endpoint = "<your-endpoint>"
key = "<your-key>"
client = DocumentIntelligenceClient(endpoint, AzureKeyCredential(key))
```

**Preguntas de auto-test:**

* ¿Qué información se obtiene del recurso de Azure Document Intelligence para conectarse al servicio?
* ¿Qué diferencias y límites existen entre los niveles de tarifa *Gratis* y *Estándar*?
* Describa brevemente cómo se usa el endpoint y la clave de acceso en el código.

<br><br><br>
## Modelos precompilados y personalizados

> **Concepto clave ➜** *Modelos precompilados* son modelos entrenados por Microsoft para tipos comunes de formulario, sin necesidad de entrenamiento extra. Un *modelo personalizado* se entrena con ejemplos específicos para extraer campos únicos.

Para documentos frecuentes (facturas, recibos, W-2, identificaciones, etc.), Document Intelligence ofrece modelos listos para usar. Estos ya están entrenados con muchos ejemplos, por lo que ofrecen resultados precisos sin que usted entrene nada.

* **Ventaja:** No es necesario proporcionar datos de entrenamiento. Úselos con llamadas simples para extraer los campos comunes de esos formularios.
* **Ejemplos:**

  * *Factura:* extrae número de pedido, fechas, totales e ítems (producto, cantidad, precio).
  * *Recibo:* extrae datos del comerciante (nombre, teléfono, dirección), totales, impuestos, fecha/hora e ítems (producto, cantidad, precio).

Si tiene formularios inusuales, entrenar un modelo personalizado mejora la precisión: proporcione al menos 5 ejemplos reales con etiquetas y use la API de entrenamiento. Un modelo personalizado aprende los pares clave-valor y estructura de esos formularios específicos.

**Preguntas de auto-test:**

* ¿Por qué y cuándo conviene usar un modelo precompilado?
* Enumere dos campos que extrae el modelo de factura precompilado.
* ¿Qué se necesita para crear y entrenar un modelo personalizado?

<br><br><br>
## Características de los modelos y entrenamiento

> **Concepto clave ➜** Los modelos precompilados extraen texto, pares clave–valor, tablas, marcas de selección y entidades de documentos.

Cada modelo de Document Intelligence está diseñado para extraer distintos datos:

* 📄 **Texto:** Todas las variantes (modelos prebuilt y custom) extraen texto escrito a mano o impreso.
* 🏷 **Pares clave-valor:** Muchos modelos detectan pares etiqueta-valor (por ejemplo, “Peso” ➜ “31 kg”).
* 📑 **Entidades:** Datos estructurados como personas, ubicaciones o fechas se extraen como entidades.
* ☑️ **Marcas de selección:** Modelos específicos identifican casillas/toggles (por ejemplo, “¿Marque X?”).
* 📊 **Tablas:** Los modelos pueden extraer tablas completas, con contenido de celdas, filas y columnas.
* **Campos fijos:** Los modelos entrenados para un formulario específico reconocen valores de campos predefinidos (por ejemplo, “Fecha de factura” en facturas).

**Entrenamiento de modelos personalizados:** Para formas propias, suba ejemplos etiquetados a un contenedor de Azure Blob (con archivos JSON de etiquetas). Cree un SAS del contenedor y luego inicie el entrenamiento (vía la API o Document Intelligence Studio). En Studio puede etiquetar visualmente. Hay dos tipos de modelos personalizados:

* **Plantilla:** Basado en reglas y OCR tradicional. Extrae con rapidez pares clave-valor, tablas, regiones, marcas de selección y firmas. Soporta >100 idiomas y su entrenamiento suele ser rápido (minutos).
* **Neuronal (Deep Learning):** Modelo de aprendizaje profundo para extraer campos etiquetados, ideal para documentos **semiestructurados** o desorganizados. Ofrece mayor precisión en casos complejos.

📌 *Clave:* elija **Plantilla** si sus formularios tienen estructuras consistentes; elija **Neuronal** para documentos variados o donde la plantilla no funcione bien.

**Preguntas de auto-test:**

* ¿Qué tipos de información (texto, tablas, etc.) pueden extraer los modelos precompilados?
* Describa brevemente las diferencias entre un modelo personalizado *de plantilla* y *neuronal*.
* Mencione dos pasos esenciales para entrenar un modelo personalizado desde cero.

<br><br><br>
## Llamadas a la API y ejemplos de código

> **Concepto clave ➜** Para usar un modelo de Document Intelligence (precompilado o personalizado), llame a la API `begin_analyze_document` (SDK) o al endpoint REST `/documentModels/{model-id}:analyze` con los datos del formulario.

Al analizar un documento, proporcione el identificador del modelo (por ejemplo, `"prebuilt-invoice"` o el ID de su modelo personalizado) y el origen de la imagen (URL o bytes). La respuesta JSON tendrá un campo `"analyzeResult"` con el contenido extraído y datos de cada página. Por ejemplo:

```python
from azure.ai.documentintelligence import DocumentIntelligenceClient
from azure.core.credentials import AzureKeyCredential

client = DocumentIntelligenceClient(endpoint, AzureKeyCredential(key))
poller = client.begin_analyze_document(
    "prebuilt-invoice", AnalyzeDocumentRequest(url_source=invoiceUrl))
result = poller.result()  
# result.documents contendrá los campos detectados (cliente, total, etc.)
```

**Atajos de código:** A continuación, una tabla resumen con ejemplos mínimos para usar Python y cURL en dos servicios de Azure AI:

| Servicio                            | Python (SDK)                                                                                                                                                                                                                                                                                                                                                                                                                                            | cURL (REST API)                                                                                                                                                                                                                                                |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Document Intelligence (factura)** | `python<br>from azure.ai.documentintelligence import DocumentIntelligenceClient<br>from azure.core.credentials import AzureKeyCredential<br>client = DocumentIntelligenceClient(endpoint, AzureKeyCredential(key))<br>poller = client.begin_analyze_document("prebuilt-invoice", AnalyzeDocumentRequest(url_source=invoiceUrl))<br>result = poller.result()`                                                                                            | `bash<br>curl -X POST "{endpoint}/documentintelligence/documentModels/prebuilt-invoice:analyze?api-version=2024-02-29" \  <br>-H "Content-Type: application/json" \  <br>-H "Ocp-Apim-Subscription-Key: <your-key>" \  <br>-d '{"urlSource":"<invoice-url>"}'` |
| **Azure AI Vision (OCR)**           | `python<br>from azure.cognitiveservices.vision.computervision import ComputerVisionClient<br>from msrest.authentication import CognitiveServicesCredentials<br>client = ComputerVisionClient(endpoint, CognitiveServicesCredentials(key))<br>read_response = client.read("https://example.com/image.jpg", raw=True)<br>operation_id = read_response.headers["Operation-Location"].split("/")[-1]<br>read_result = client.get_read_result(operation_id)` | `bash<br>curl -X POST "{vision_endpoint}/vision/v3.2/ocr?language=es&detectOrientation=true" \  <br>-H "Content-Type: application/json" \  <br>-H "Ocp-Apim-Subscription-Key: <your-key>" \  <br>-d '{"url":"<image-url>"}'`                                   |

*Nota:* En cURL reemplace `{endpoint}` y `{vision_endpoint}` por el URL de sus recursos y `<your-key>` por su clave. Los resultados de OCR devuelven texto de la imagen en JSON. Para Document Intelligence, la respuesta incluirá campos e índices con sus valores.

**Preguntas de auto-test:**

* ¿Cómo especifica el modelo a usar en una solicitud de análisis de documentos?
* ¿Qué contiene la respuesta JSON (`analyzeResult`) de Document Intelligence?
* ¿Qué HTTP headers son obligatorios en las llamadas REST a estos servicios?

<br><br><br>
## Modelos compuestos

> **Concepto clave ➜** Un *modelo compuesto* combina varios modelos personalizados para analizar múltiples tipos de formularios con una sola llamada.

Después de entrenar varios modelos personalizados (por ejemplo, uno por cada versión de un formulario), ensámblelos en un modelo compuesto. Esto se puede hacer en Document Intelligence **Studio** (GUI) o por código (método `begin_create_composed_model`). Al enviar un formulario, especifique el ID del modelo compuesto. El resultado incluirá `docType` indicando cuál de los sub-modelos fue aplicado.

⚠️ **Límites y compatibilidades:** En el nivel Estándar S0 puede crear hasta 200 modelos compuestos en una suscripción. Un único modelo compuesto puede contener **hasta 100** modelos personalizados. No se pueden mezclar tipos: los modelos *de plantilla* solo se combinan con otros de plantilla, y los *neurales* solo con neurales.

**Preguntas de auto-test:**

* ¿Cuál es el propósito de un modelo compuesto en Document Intelligence?
* ¿Qué indica el campo `docType` en el resultado de un análisis con modelo compuesto?
* Nombre una restricción al crear modelos compuestos (ej. límite de modelos).

<br><br><br>
## Glosario

* **Azure AI Document Intelligence:** Servicio en la nube de Azure para extraer datos estructurados de documentos y formularios.
* **OCR (Optical Character Recognition):** Tecnología que convierte imágenes de texto en texto editable; Azure Vision ofrece OCR básico.
* **Endpoint:** URL pública del recurso de Azure usada para llamadas API.
* **Clave de acceso (API Key):** Cadena secreta asociada al recurso que autentica las llamadas API.
* **JSON:** Formato de texto ligero usado para datos; resultado de Document Intelligence se entrega en JSON.
* **Modelo precompilado:** Modelo proporcionado por Microsoft, entrenado para tipos comunes (facturas, recibos, etc.); no requiere entrenamiento extra.
* **Modelo personalizado:** Modelo que usted entrena usando ejemplos de sus formularios, para extraer campos específicos de documentos inusuales.
* **Modelo compuesto:** Modelo que agrupa varios modelos personalizados, permitiendo analizar diferentes tipos de formulario con una sola llamada.
* **Pares clave-valor:** Elementos extraídos que relacionan una *clave* (etiqueta) con su *valor* en el documento.
* **Tablas:** Estructuras de filas/columnas detectadas dentro del documento.
* **Marca de selección:** Elemento como casilla o botón de opción (checkbox/radio) que puede estar marcado o no.
* **Azure Blob Storage:** Servicio de Azure para almacenar ficheros; se usa comúnmente para alojar imágenes de entrenamiento y etiquetas para modelos personalizados.
* **Document Intelligence Studio:** Interfaz visual de Azure para probar, etiquetar y entrenar modelos sin escribir código.
* **SAS (Shared Access Signature):** URL segura que da acceso temporal a un recurso de almacenamiento de Azure (como contenedores de blobs).
* **Claves de usuario y suscripción:** Métodos de autenticación; FormRecognizer admite claves (AzureKeyCredential) o token AAD.
* **Azure Cognitive Services:** Conjunto de servicios de IA en Azure, entre ellos Document Intelligence y Computer Vision.

**Tabla resumen (flashcards):**

| Concepto / Pregunta                          | Respuesta clave                                                                                                                                                                         | A memorizar                                                                     |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **¿Qué es Azure AI Document Intelligence?**  | Servicio de Azure para analizar documentos y extraer datos estructurados automáticamente.                                                                                               | Servicio IA que automatiza extracción.                                          |
| **Modelos precompilados vs personalizados**  | *Precompilados* están entrenados por Microsoft para documentos comunes (no requieren entrenamiento). *Personalizados* se entrenan con sus datos específicos para extraer campos únicos. | Precompilado: listo para usar. Personalizado: requiere entrenamiento.           |
| **Campos extraídos de una factura**          | Cliente, fechas (factura/vencimiento), totales, impuestos e ítems (producto, cantidad, precio).                                                                                         | Cliente, total factura, ítems.                                                  |
| **Campos extraídos de un recibo**            | Comerciante (nombre, teléfono, dirección), total (incluye impuestos, propinas), fecha/hora e ítems (producto, cantidad, precio).                                                        | Total pagado, impuestos, ítems.                                                 |
| **¿Qué hace el modelo *Documento general*?** | Extrae texto, pares clave-valor y tablas de documentos en general.                                                                                                                      | Clave-valor y tablas en documentos libres.                                      |
| **Plantilla vs Neuronal**                    | Plantilla: rápido, +100 idiomas, bueno en formularios estructurados. Neuronal: deep learning, mejor para documentos *semiestructurados*.                                                | Plantilla: rápido, varios idiomas. Neuronal: aprende mejor documentos variados. |
| **¿Para qué sirve un *modelo compuesto*?**   | Permite enviar diferentes tipos de formulario a un único modelo que redirige al sub-modelo adecuado (muestra en `docType`).                                                             | Combinar modelos para múltiples formularios.                                    |
| **Conexión (endpoint + key)**                | Debe usar el endpoint del recurso y la clave de acceso en el cliente o en el header (`Ocp-Apim-Subscription-Key`) para autenticar cada solicitud.                                       | Endpoint URL y API key en cada llamada.                                         |
| **¿Qué contiene `analyzeResult` en JSON?**   | Contiene `content` (texto completo) y una lista de páginas con campos extraídos y sus coordenadas/confianza.                                                                            | Resultado en JSON con campos extraídos.                                         |
| **Visión vs Document Intelligence**          | Visión OCR sólo extrae texto plano de imágenes. Document Intelligence extrae además estructura (KVP, tablas, campos).                                                                   | Document Intelligence = OCR + contexto.                                         |
