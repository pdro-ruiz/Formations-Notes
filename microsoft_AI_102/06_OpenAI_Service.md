# Desarrollo de soluciones con Azure OpenAI Service

> 🗝️ **Concepto clave ➜** Azure OpenAI Service es un servicio en la nube que ofrece modelos de lenguaje generativos (como GPT-3/4, *embeddings* y DALL·E) dentro de la plataforma Azure.

Azure OpenAI Service permite acceder a modelos de lenguaje avanzados de OpenAI (como GPT-3.5, GPT-4, incrustaciones de texto, DALL·E, etc.) desde Azure. Estos modelos pueden **comprender, generar y manipular texto, código o imágenes** en base a indicaciones en lenguaje natural. Por ejemplo, ChatGPT es un bot que usa un modelo GPT-4 para procesar preguntas y **responder con texto de apariencia humana**. Al integrar estos modelos en Azure, las soluciones heredan ventajas de seguridad, escalabilidad e integración con otros servicios de la plataforma.

* 🔍 *Ejemplo:* Para crear un chatbot de soporte técnico que resuma información y sugiera código, usaríamos Azure OpenAI con prompts similares a los de ChatGPT.
* 📌 Azure OpenAI Service se accede vía **API REST**, **SDKs** (Python, C#, etc.) o la interfaz web de **Azure AI Studio/Foundry**.

**Autoevaluación:**

* ¿Qué es Azure OpenAI Service y qué modelos incluye?
* ¿Cómo se relaciona ChatGPT con Azure OpenAI Service?

<br><br><br>
## Acceso a Azure OpenAI Service

> 🗝️ **Concepto clave ➜** Para usar Azure OpenAI debes crear (aprovisionar) un *recurso* en tu suscripción de Azure.

El primer paso es **provisionar un recurso de Azure OpenAI** en Azure. Esto se puede hacer mediante el portal web de Azure o usando la CLI de Azure. Al crearlo, debes indicar la suscripción, grupo de recursos, región, un nombre único para el recurso y el plan de tarifa. Por ejemplo, con la CLI se usaría un comando como:

```bash
az cognitiveservices account create \
  -n <NombreÚnico> \
  -g <MiGrupo> \
  -l <Región> \
  --kind OpenAI \
  --sku S0 \
  --subscription <MiSuscripción>
```

Este comando creará un recurso de tipo OpenAI en la región especificada.

* 🛠️ *Atajo de código:* En Python no hay una librería especial para crear el recurso (usa CLI o Azure SDK).
* 🔑 El recurso de Azure OpenAI funcionará como contenedor donde implementas los modelos.

Una vez creado, podrás acceder al servicio desde **Azure AI Studio** (portal [https://ai.azure.com](https://ai.azure.com)) o directamente desde tu código usando el *endpoint* y la *clave API* del recurso. Si otros usuarios lo usan, necesitan roles de OpenAI (`Usuario de OpenAI` o `Colaborador de OpenAI`).

**Autoevaluación:**

* ¿Qué datos pide Azure al crear un recurso de OpenAI?
* Menciona dos formas de crear un recurso de Azure OpenAI (portal vs CLI).

<br><br><br>
## Azure AI Foundry y Catálogo de modelos

> 🗝️ **Concepto clave ➜** **Azure AI Foundry (AI Studio)** es la interfaz web donde gestionas despliegues de modelos generativos en Azure.

Después de crear el recurso, ingresa a **Azure AI Studio**. Ahí eliges tu directorio y suscripción, y luego el recurso de Azure OpenAI correspondiente. En la sección **Azure OpenAI** verás el **Catálogo de modelos**: una lista de modelos base disponibles (por ejemplo GPT-4, GPT-3.5, DALL·E) que puedes seleccionar. Desde allí creas despliegues (implementaciones) de modelo base para usarlos.

👥 **Roles necesarios:** Si no eres dueño del recurso, necesitas el rol **Usuario de OpenAI** (para ver recursos y probar en el playground) y **Colaborador de OpenAI** (para crear implementaciones).

**Autoevaluación:**

* ¿Qué es Azure AI Studio (Foundry) y para qué se usa?
* ¿Qué significa que un modelo en el catálogo esté en estado "Correcto"?

<br><br><br>
## Tipos de modelos disponibles

> 🗝️ **Concepto clave ➜** Azure OpenAI ofrece modelos de lenguaje (GPT-4, GPT-3.5), incrustaciones, y modelos especializados (DALL·E, Whisper, etc.).

Azure OpenAI incluye varios tipos de modelo:

* 🤖 **GPT-4:** El modelo de última generación para **texto y código**. Genera respuestas avanzadas basadas en prompts de lenguaje natural.
* 🤖 **GPT-3.5 (GPT-35-turbo):** Modelo versátil para texto y código, optimizado para chat conversacional. Funciona bien en la mayoría de escenarios de IA generativa.
* 🧮 **Incrustaciones (Embeddings):** Convierte texto en vectores numéricos. Útil para análisis de similitud de texto, búsqueda semántica, agrupamiento, etc..
* 🎨 **DALL·E:** Modelo para **generar imágenes** a partir de descripciones de lenguaje natural. Actualmente en vista previa, puede crear imágenes originales basadas en tu prompt.
* 🎙️ **Whisper:** Modelo de **transcripción de voz a texto**. Convierte grabaciones de audio en texto escrito.
* 🔊 **Texto a voz:** Modelos que convierten texto en voz hablada de alta calidad.

> **Nota:** Los precios dependen del número de tokens procesados y del tipo de modelo. También ten en cuenta que **no todos los modelos** están disponibles en todas las regiones.

**Autoevaluación:**

* ¿Para qué se usan los modelos de incrustaciones (embeddings)?
* Menciona dos usos posibles de DALL·E.


<br><br><br>
## Implementación de modelos en Azure OpenAI

> 🗝️ **Concepto clave ➜** Una vez seleccionado un modelo base, debes **desplegarlo (implementarlo)** en tu recurso Azure OpenAI para poder usarlo.

Antes de hacer peticiones, implementa el modelo elegido. Puedes crear varias implementaciones (copias) de un mismo modelo base, siempre que no excedas tu cuota de tokens por minuto. Hay tres métodos principales:

* 🌐 **Azure AI Studio (portal):** En el Catálogo de modelos, elige un modelo base y dale un nombre para desplegarlo.
* 💻 **CLI de Azure:** Con comandos como `az cognitiveservices account deployment create` configuras un despliegue vía línea de comandos. Ejemplo mínimo:

  ```bash
  az cognitiveservices account deployment create \
    -g MiGrupo \
    -n MiRecurso \
    --deployment-name MiModelo \
    --model-name gpt-35-turbo \
    --model-version "0125" \
    --model-format OpenAI \
    --sku-name "Standard" \
    --sku-capacity 1
  ```

  Este comando implementa `gpt-35-turbo` (versión 0125) en tu recurso.
* 🔗 **API REST:** Puedes llamar directamente a la API REST de implementación para crear un despliegue desde tu aplicación. En la solicitud especificas el modelo base deseado (consulta la documentación oficial).

Cada implementación tiene un nombre único (*deployment name*) que usarás luego en las llamadas API.

**Autoevaluación:**

* ¿Qué información necesitas proporcionar al implementar un modelo mediante CLI?
* ¿Qué ventajas tiene usar el portal (Studio) en vez de la CLI para desplegar modelos?

<br><br><br>
## Tipos de solicitudes (*prompts*) y tareas

> 🗝️ **Concepto clave ➜** Un *prompt* o solicitud es el mensaje de entrada que das al modelo; con él defines la tarea que quieres (clasificar, generar, traducir, resumir, etc.).

Las solicitudes se pueden clasificar según la tarea deseada. Algunos ejemplos:

* 📝 **Clasificación de contenido:** P. ej., dado un tweet, determinar si la opinión es *positiva* o *negativa*.
* 📄 **Generación de contenido:** P. ej., pedir al modelo que liste “Formas de viajar” genera un listado de opciones.
* 💬 **Conversación:** El modelo mantiene un diálogo. Envíale un historial de chat y el siguiente turno del usuario, y responde como asistente.
* 🔄 **Transformación o traducción:** P. ej., convertir “Hola” a francés produce “Bonjour”.
* 📑 **Resumen:** P. ej., pedir “Resume este texto…” y el modelo devolverá un resumen del contenido dado.
* 🚀 **Continuación de texto:** Dado “Una manera de cultivar tomates es plantar semillas…”, el modelo sigue el texto a partir de allí.
* ❓ **Preguntas y respuestas fácticas:** P. ej., “¿Cuántas lunas tiene la Tierra?” produce “Uno”.

La **calidad de la respuesta** generada depende de varios factores, entre ellos:

* La forma en que diseñas el prompt (cómo escribes la petición al modelo).
* Los parámetros del modelo (ver la sección de abajo).
* Los datos en los que el modelo fue entrenado (o adaptados mediante *fine-tuning*).

👀 *Consejo:* Experimenta con diferentes prompts en el Azure AI Studio Playground antes de integrarlo en tu app.

**Autoevaluación:**

* Da un ejemplo de prompt para una tarea de resumen y otro para clasificación de sentimiento.
* ¿Qué factores afectan la calidad de la generación de texto?

<br><br><br>
## Puntos de conexión y llamadas API

> 🗝️ **Concepto clave ➜** Una vez implementado un modelo en Azure, interactúas con él mediante **endpoints (puntos de conexión)**. Los principales son **ChatCompletion**, **Completions** y **Embeddings**.

Para usar el modelo desde tu aplicación, necesitas: el **endpoint** de tu recurso, tu **clave API** y el **nombre de la implementación** (deployment) que creaste. Con estos, puedes hacer solicitudes HTTP al servicio. Los endpoints más comunes son:

* 🖥️ **Completions:** Envías un prompt de texto y el modelo genera uno o varios *completions* (finalizaciones) de texto. Este endpoint es para modelos de GPT-3 clásicos (no optimizados para chat).
* 💬 **ChatCompletion:** Envías una conversación en formato JSON con roles (`system`, `user`, `assistant`), y el modelo responde con el siguiente mensaje del chat. Por ejemplo, puedes inicializar la conversación con un *mensaje del sistema* para definir el rol del asistente, y luego enviar mensajes de usuario. Este endpoint es el más usado con modelos GPT-4 y GPT-3.5-turbo.
* 📈 **Embeddings:** Envías texto y el modelo devuelve un vector de números (embedding) que representa el significado del texto. Úsalo para comparaciones de similitud o indexación semántica.

🌐 *Ejemplo de ChatCompletion (curl):* enviar una conversación de entrenamiento:

```bash
curl https://<YOUR_ENDPOINT>.openai.azure.com/openai/deployments/<DEPLOY_NAME>/chat/completions?api-version=2023-03-15-preview \
  -H "Content-Type: application/json" \
  -H "api-key: <YOUR_API_KEY>" \
  -d '{
        "messages":[
          {"role": "system", "content": "Eres un asistente amigable enseñando sobre IA."},
          {"role": "user", "content": "¿Cuál es la última versión de modelos GPT en Azure?"}
        ]
      }'
```

El modelo responderá con un JSON que incluye la respuesta del asistente.

👩‍💻 Para *obtener embeddings*, se hace una solicitud similar al endpoint `/embeddings`:

```bash
curl https://<YOUR_ENDPOINT>.openai.azure.com/openai/deployments/<DEPLOY_NAME>/embeddings?api-version=2022-12-01 \
  -H "Content-Type: application/json" \
  -H "api-key: <YOUR_API_KEY>" \
  -d '{"input": "Prueba de embeddings"}'
```

Se devuelve un JSON con la lista de vectores (uno por entrada enviada).

**Tabla de atajos de código (ejemplos mínimos):**

| Endpoint                   | Python (biblioteca OpenAI)                                                                                                                                                                                                                                                                  | Curl                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **ChatCompletion** (texto) | `python\nimport openai\nopenai.api_key="<YOUR_API_KEY>"\nopenai.api_base="https://<YOUR_ENDPOINT>.openai.azure.com/"\nresp = openai.ChatCompletion.create(\n    model="<DEPLOY_NAME>",\n    messages=[{\"role\":\"user\",\"content\":\"Hola\"}]\n)\nprint(resp.choices[0].message.content)` | Como arriba en el ejemplo de *curl*.                                                 |
| **Embeddings**             | `python\nembedding = openai.Embedding.create(\n    engine=\"<DEPLOY_NAME>\",\n    input=\"El texto a vectorizar\"\n)\nvector = embedding.data[0].embedding\n`                                                                                                                               | Como arriba: endpoint `/embeddings` con el JSON `{"input":"El texto a vectorizar"}`. |

**Autoevaluación:**

* ¿Qué diferencia hay entre los endpoints **Completions** y **ChatCompletions**?
* Menciona qué información necesitas para llamar al API REST de Azure OpenAI (endpoint, clave, deployment).

<br><br><br>
## Uso del SDK de Azure OpenAI

> 🗝️ **Concepto clave ➜** Existen SDKs específicos (por ejemplo, la biblioteca `openai` de Python) que facilitan el uso de Azure OpenAI desde código.

Además de las llamadas REST directas, puedes usar el SDK oficial de Python (mantenido por OpenAI) o bibliotecas para C#, JavaScript, etc. Estos SDKs envuelven las peticiones HTTP y ofrecen métodos sencillos. Para Python: instala la librería con `pip install openai`, luego configuras el cliente con tu endpoint y clave. Ejemplo básico:

```python
from openai import OpenAI

client = OpenAI(azure_api_key="<YOUR_API_KEY>", azure_api_base="<YOUR_ENDPOINT>", api_type="azure")
resp = client.chat.completions.create(
    model="<DEPLOY_NAME>",
    messages=[
        {"role": "system", "content": "Eres un asistente amigable."},
        {"role": "user", "content": "¿Qué es Azure OpenAI?"}
    ]
)
print(resp.choices[0].message.content)
```

Esta llamada es equivalente a la REST anterior, pero usando la biblioteca. El objeto de respuesta (`resp`) contendrá la respuesta generada, el uso de tokens, etc. Desde Python o C# también puedes ajustar parámetros opcionales como `temperature` o `max_tokens` al llamar al método.

**Autoevaluación:**

* ¿Cómo se inicializa el cliente de OpenAI en Python para Azure OpenAI (qué datos pide)?
* ¿Qué biblioteca usas para consumir Azure OpenAI en Python, y cómo se instala?

<br><br><br>
## Ingeniería de prompts (ingeniería de avisos)

> 🗝️ **Concepto clave ➜** La **ingeniería de prompts** es el arte de redactar la solicitud (prompt) de forma clara y estructurada para obtener respuestas precisas y útiles.

La calidad de lo que recibe el modelo depende en gran parte de **cómo le preguntas**. Algunas buenas prácticas:

* ✍️ **Instrucciones claras y detalladas:** Explica con detalle lo que quieres. Por ejemplo, al generar la descripción de un producto, decir *“escribe una descripción detallada que mencione materiales ecológicos”* produce un resultado más concreto que solo *“describe este producto”*.
* 🔄 **Formato y estructura:** Puedes pedir que la salida tenga cierto formato. P. ej., “Escribe una tabla en Markdown con 6 animales, indicando su género y especie” produce tablas estructuradas.
* 📌 **Contenido principal vs complementario vs base:**   Incluye primero el *contenido principal* (lo que quieres procesar, p.ej., un texto para resumir) separado del prompt, y luego instrucciones. Añade *contenido complementario* (ej. “Estoy interesado en IA y fechas de webinars” en un correo) para guiar al modelo sobre qué buscar. Si quieres respuestas basadas en información específica, usa *contenido de base* (por ejemplo, un artículo científico) para “anclar” la respuesta a esos datos.
* 🧑‍💼 **Mensaje del sistema:** En `ChatCompletion`, el primer mensaje puede tener rol `system` para definir el tono o rol del asistente. P. ej., “Actúa como traductor inglés-español, solo traduce el texto”. El modelo seguirá estas instrucciones al responder.
* 🕰️ **Sesgo de recencia:** En prompts largos, la información al final suele influir más en la respuesta. Experimenta repitiendo instrucciones claves al final si es necesario. En chats, los mensajes recientes del historial afectan más la respuesta.
* ℹ️ **Mostrar contexto con ejemplos:** Cuando pidas algo complejo, a veces es útil dar ejemplos o notas al modelo en el prompt para guiar su salida.

**Ejemplos prácticos:**

* Pedir instrucciones claras mejoró notablemente la respuesta (segunda petición incluye más detalles):

  **Aviso simple:** “Describe esta botella de agua”
  **Respuesta:** texto genérico sobre botella.

  **Aviso detallado:** “Describe esta botella de agua 100% reciclada, menciona colores naturales, y que cada compra elimina 10 libras de plástico del océano.”
  **Respuesta:** descripción específica incluyendo reciclaje y beneficios ambientales.

* Pide formato estructurado:
  Aviso: “Escribe una tabla de 6 animales con género y especie.”
  Respuesta: tabla en Markdown con filas de animales.

**Autoevaluación:**

* ¿Qué contiene típicamente un *mensaje del sistema* y para qué sirve?
* Explica la diferencia entre **contenido principal** y **contenido de base**.

<br><br><br>
## Parámetros del modelo

> 🗝️ **Concepto clave ➜** Los parámetros como **`temperature`** y **`top_p`** controlan la aleatoriedad de las respuestas.

Azure OpenAI permite afinar el comportamiento del modelo vía parámetros opcionales en la llamada API:

* 🎲 **`temperature`** (0.0 a 1.0+): Controla la creatividad. Un valor bajo (p.ej. 0.2) hace que la respuesta sea más **determinística y coherente**, repitiendo respuestas comunes. Un valor alto (p.ej. 0.8) produce respuestas más **variadas y creativas**.
* 🔢 **`top_p`** (nuclear sampling): Ajusta la probabilidad acumulada de las palabras. Reduce el vocabulario de salida. Un valor alto también aumenta la diversidad léxica.
* 💠 **Tokens máximos (`max_tokens`)**: Limita la longitud de la respuesta.
* Otros parámetros: `frequency_penalty`, `presence_penalty`, etc., para pulir el estilo.

> *Consejo:* Ajusta `temperature` y `top_p` por separado para ver su efecto. Valores altos dan resultados más imaginativos pero menos enfocados.

**Autoevaluación:**

* ¿Qué efecto tiene aumentar la temperatura en la generación de texto?
* ¿Cuándo podrías querer un `temperature` bajo?

<br><br><br>
## Fine-tuning vs RAG (OpenAI en los datos)

> 🗝️ **Concepto clave ➜** El **ajuste fino** (fine-tuning) entrena un modelo base con tus datos, mientras que **RAG** (Retrieval-Augmented Generation) conecta el modelo a tus datos sin entrenar.

Azure OpenAI ofrece dos estrategias para incorporar datos específicos:

* 🛠 **Fine-tuning:** Reentrena un modelo básico existente (p.ej. GPT-35-turbo) con tu propio conjunto de entrenamiento. Esto puede mejorar las respuestas para tu caso de uso concreto y manejar contextos grandes. Sin embargo, **es costoso y consume mucho tiempo**. Se usa solo cuando es necesario un modelo altamente personalizado.

* 📚 **RAG (*en los datos*):** No entrena modelo nuevo. En su lugar, cada vez que envías un prompt, primero **buscas información** relevante en tus datos (por ejemplo, usando Azure Cognitive Search) y luego *inyectas* esos datos en el prompt al modelo. De esta forma el modelo genera respuestas basadas en datos actualizados sin cambiar el modelo básico.

Ejemplo: un asistente que responde usando documentos de tu empresa. Con RAG, Azure AI busca pasajes relacionados y los agrega al prompt antes de llamar al modelo.

**Autoevaluación:**

* ¿Qué ventaja tiene RAG frente al ajuste fino?
* ¿Por qué el ajuste fino solo se recomienda en casos necesarios?

<br><br><br>
## Conexión de datos (*RAG con datos propios*)

> 🗝️ **Concepto clave ➜** Azure AI Studio permite conectar tus propios datos (archivos, índices de búsqueda) para usarlos en prompts con Azure OpenAI.

Para usar RAG con tus datos, sigue estos pasos:

1. **Conectar datos en AI Studio:** En Azure AI Studio, ve al playground de chat y selecciona la pestaña **Agregar datos**. Sigue el asistente para cargar archivos (.md, .txt, .pdf, .docx, etc.) o conectar a un índice de búsqueda existente. El sistema creará un índice semántico de tu contenido.
2. **Uso en el prompt:** Al chatear, el sistema busca partes relevantes de tus datos (sobre la pregunta) y las incluye en el mensaje. De este modo, cuando envías el prompt al modelo, le estás dando contexto actualizado de tus fuentes.
3. **Llamada API con datos:** Si programas tu propia app, en la petición JSON incluyes un objeto `dataSources` con la dirección de tu servicio de Azure Cognitive Search, su clave y `indexName`. Por ejemplo:

```json
{
  "dataSources": [
    {
      "type": "AzureCognitiveSearch",
      "parameters": {
        "endpoint": "<tu_search_endpoint>",
        "key": "<tu_search_key>",
        "indexName": "<tu_indice>"
      }
    }
  ],
  "messages": [
    {"role": "system", "content": "Eres un asistente de viajes."},
    {"role": "user", "content": "Quiero ir a Nueva York. ¿Dónde me quedo?"}
  ]
}
```

El servicio enviará esta petición al endpoint de chat de tu modelo. Azure buscará información relevante en el índice y la usará para mejorar la respuesta del modelo.

**Consideraciones de tokens:** Al usar RAG, se incluyen tokens del mensaje del sistema, el historial, los fragmentos recuperados de los datos, etc. Es importante **acotar la longitud** de las preguntas y del historial para no exceder el límite del modelo. Por ejemplo, el mensaje del sistema se trunca si supera el límite de tokens. El modelo limita su respuesta a 1500 tokens cuando usas datos propios.

**Autoevaluación:**

* ¿Qué tipos de archivo puedes cargar en Azure AI Studio para RAG?
* ¿Qué información debes incluir en la llamada API para usar tus datos conectados con el modelo?


<br><br><br>
## Generación de imágenes con Azure OpenAI (DALL·E)

> 🗝️ **Concepto clave ➜** DALL·E es el modelo de Azure OpenAI que **genera imágenes** originales a partir de una descripción en lenguaje natural.

El servicio Azure OpenAI permite usar modelos de OpenAI para gráficos a través de DALL·E. Puedes crear ilustraciones, diseños de productos o cualquier imagen única descrita por texto.

**¿Qué es DALL·E?** Es una red neuronal entrenada para generar imágenes a partir de texto. Por ejemplo, el prompt *“Una ardilla en una motocicleta”* podría producir una imagen similar a la siguiente:

![Ejemplo de imagen generada: ardilla en motocicleta](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/images/dall-e-squirrel-motorcycle.png)

> **Nota:** Las imágenes creadas por DALL·E son originales, no extraídas de un catálogo. El modelo genera nuevas imágenes basadas en lo que ha aprendido.

Para probar DALL·E en el **Azure AI Studio**, ve al área de juegos *Imágenes*. Ahí puedes escribir prompts de texto y ajustar parámetros como **resolución** (1024×1024, 1792×1024, etc.), **estilo** (natural o vívido) y **calidad** (estándar o HD).

**Uso de la API REST para DALL·E:** Al igual que con texto, usas una llamada POST. El JSON de solicitud incluye al menos:

* `prompt`: la descripción de la imagen.
* `n`: cuántas imágenes generar (DALL·E 3 admite solo 1).
* `size`: resolución (e.g. `"1024x1024"`).
* Opcionales: `quality` (`"standard"` o `"hd"`, por defecto estándar) y `style` (`"natural"` o `"vivid"`, por defecto vívido).

Ejemplo de JSON para un escudo con esmoquin:

```json
{
  "prompt": "Un tejón usando esmoquin",
  "n": 1,
  "size": "512x512",
  "quality": "hd",
  "style": "vivid"
}
```

Con DALL·E 3, la respuesta llega **síncronamente** e incluye la URL de la imagen generada. Ejemplo de respuesta:

```json
{
  "created": 1686780744,
  "data": [
    {
      "url": "<URL de la imagen generada>",
      "revised_prompt": "A badger wearing a tuxedo"
    }
  ]
}
```

Luego puedes descargar la imagen PNG usando esa URL. Por ejemplo, el prompt anterior podría producir una imagen como la de abajo (un tejón con esmoquin):

<p align="center"> <img src="https://learn.microsoft.com/en-us/azure/cognitive-services/openai/images/dall-e-badger-tuxedo.png" alt="Tejón con esmoquin generado por DALL·E"> </p> 

**Autoevaluación:**

* ¿Qué parámetros mínimos pide la API de DALL·E para generar una imagen?
* ¿Cómo difiere la respuesta de la API entre DALL·E 2 y DALL·E 3 según el flujo descrito?

<br><br><br>
## Mini-glosario

* **Azure OpenAI Service:** Servicio en la nube que ofrece modelos generativos de OpenAI en la plataforma Azure.
* **Implementación (Deployment):** Despliegue de un modelo base en tu recurso de Azure OpenAI (por ejemplo, “gpt35turbo”) para usarlo.
* **Prompt (Aviso):** La entrada de texto (instrucción) que envías al modelo para guiar la generación de la respuesta.
* **ChatCompletion:** Endpoint de API donde envías un diálogo (mensajes con roles) y obtienes la siguiente respuesta conversacional.
* **Completions:** Endpoint de API donde envías texto libre y recibes texto continuado (usado con modelos GPT-3 clásicos).
* **Embeddings (Incrustaciones):** Representaciones vectoriales de texto; útiles para medir similitud o indexar contenido.
* **Fine-tuning (Ajuste fino):** Entrenamiento adicional de un modelo base con tus datos específicos.
* **RAG (En los datos):** Técnica que busca información relevante en tus datos externos (p. ej. Azure Cognitive Search) y la inyecta en el prompt en cada petición.
* **Token:** Unidad básica de texto procesada por el modelo (por ejemplo, cada palabra o parte de palabra). Los precios de Azure OpenAI se calculan por token procesado.
* **Temperature:** Parámetro que controla aleatoriedad en la generación; valores más altos = más creativas/variadas las respuestas.
* **Azure AI Studio (Foundry):** Interfaz web de Azure para gestionar e implementar modelos generativos, así como experimentar con ellos (playground).
* **Modelo base:** Un modelo preentrenado estándar provisto por Microsoft (GPT-35, GPT-4, DALL·E, etc.) sobre el cual se basan tus implementaciones.

<br><br><br>
## Tabla resumen (Flashcards)

| Servicio/Funcionalidad          | Descripción breve                                                                   | ¡A memorizar!                            |
| ------------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------- |
| **Azure OpenAI Service**        | Plataforma Azure con modelos generativos de OpenAI (GPT, DALL·E, etc.).             | Modelos GPT/Ey no comparten datos.       |
| **ChatCompletion**              | Endpoint para conversaciones: envía historial con roles y recibe respuesta de chat. | ChatGPT en Azure → *Mensajes con roles*. |
| **Completions**                 | Endpoint para completar texto simple: envías prompt y recibe texto generado.        | Usado en modelos GPT-3 clásicos.         |
| **Embeddings**                  | Convierte texto en vectores numéricos. Útil para búsquedas semánticas.              | *Texto → vectores* para similitud.       |
| **DALL·E**                      | Modelo para crear imágenes desde texto.                                             | Prompt de texto → imagen PNG.            |
| **endpoint (punto final)**      | URL del recurso Azure OpenAI más ruta específica (ej. `/chat/completions`).         | Es parte de la URL de la petición.       |
| **Deployment (implementación)** | Nombre único dado a un modelo desplegado (ej. “gpt35turbo”).                        | Lo usan en API para identificar modelo.  |
| **temperature**                 | Parámetro (0–1+) que ajusta creatividad: *bajo* = coherente, *alto* = creativo.     | Controla variabilidad.                   |
| **Prompt (aviso)**              | Instrucción o entrada textual al modelo.                                            | Redactarlo claro y detallado.            |
| **Fine-tuning (ajuste fino)**   | Retraining de un modelo con datos propios.                                          | Solo si necesitas personalización.       |
| **RAG (retrieval)**             | Uso de búsquedas en datos propios + IA, sin entrenar modelo.                        | Injecta datos externos al prompt.        |
| **Azure AI Studio**             | Portal web para implementar modelos y probar prompts (playground).                  | Punto de partida visual.                 |
