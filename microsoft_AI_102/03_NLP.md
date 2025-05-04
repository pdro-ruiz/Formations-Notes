# Desarrollo de soluciones NLP con Azure AI

**Azure AI Language** es un servicio en la nube de Microsoft que permite a las aplicaciones entender el lenguaje humano (texto) de forma inteligente. Sin necesidad de ser un experto en IA, puedes usar **Azure AI Language** para analizar textos y obtener información como el idioma en que están escritos, el sentimiento que expresan, las ideas principales que contienen, las entidades (nombres propios, lugares, etc.) mencionadas y hasta vincular esos nombres con referencias conocidas. A continuación, presentamos cada funcionalidad clave de Azure AI Language de manera clara y educativa, con ejemplos prácticos y breves para que cualquier persona (incluso sin conocimientos técnicos) pueda entender cómo funcionan. ¡Comencemos!

<br><br><br>
## Detección de idioma

📌 **Concepto clave ➜** Identificación automática del idioma principal de un texto, indicando cuán segura está la IA de su predicción.

La **detección de idioma** analiza un texto dado y determina en qué idioma está escrito. Por cada documento de entrada, la API devuelve el idioma identificado (por ejemplo, Español, Inglés, Francés) junto con una **puntuación de confianza** (entre 0 y 1) que indica la seguridad del modelo en esa predicción.

Esta capacidad es muy útil cuando no sabemos de antemano el idioma de un contenido, por ejemplo:

* Bases de datos o almacenes con documentos **multilingües** (textos en varios idiomas mezclados).
* **Chatbots** o aplicaciones que necesitan adaptarse automáticamente al idioma del usuario.

**Cómo funciona:** Puedes enviar uno o varios textos en una sola solicitud. El servicio detectará el idioma de cada texto individualmente.

* ⚠️ **Límites:** Cada documento de texto puede tener hasta **5120 caracteres** y se pueden enviar hasta **1000 documentos** en una sola solicitud (lote).
* 💡 **Tip opcional:** Se puede proporcionar una pista geográfica (`countryHint`) para ayudar a afinar la detección (por ejemplo, indicar “US” o “ES” si se conoce el país de origen del texto), aunque no es obligatorio.

**Ejemplo de solicitud (REST JSON):** Queremos detectar el idioma de un saludo sencillo. Enviamos un JSON indicando el tipo de análisis (`"kind": "LanguageDetection"`) y el texto.

```json
{
  "kind": "LanguageDetection",
  "analysisInput": {
    "documents": [
      { "id": "1", "text": "Hola mundo" }
    ]
  }
}
```

Al hacer una llamada HTTP POST a la API con este cuerpo (junto con nuestro endpoint de Azure y clave de suscripción), el servicio responderá con el idioma detectado para cada documento.

**Ejemplo de respuesta (JSON):** La respuesta incluirá el idioma identificado y la puntuación de confianza. Por ejemplo, para el texto anterior podría ser:

```json
{
  "id": "1",
  "detectedLanguage": {
    "name": "Spanish",
    "iso6391Name": "es",
    "confidenceScore": 0.99
  }
}
```

En este caso, la API identificó **Español** (`"name": "Spanish"`, código `"es"`) con una alta confianza (⭐ `confidenceScore` \~0.99, muy cercano a 1).

**Ejemplo de código en Python (usando `requests`):** A continuación, mostramos cómo sería llamar a la API de detección de idioma desde Python. En el código, reemplaza `<YOUR_ENDPOINT>` por el URL endpoint de tu servicio y `<YOUR_KEY>` por tu clave de suscripción:

```python
import requests

endpoint = "<YOUR_ENDPOINT>/language/analyze-text?api-version=2022-10-01"
api_key = "<YOUR_KEY>"

# Estructuramos la solicitud en formato JSON
request_data = {
    "kind": "LanguageDetection",
    "analysisInput": {
        "documents": [
            { "id": "1", "text": "Hola mundo" }
        ]
    }
}

# Cabeceras de la petición, incluyendo la clave de suscripción y el tipo de contenido
headers = {
    "Ocp-Apim-Subscription-Key": api_key,
    "Content-Type": "application/json"
}

# Realizar la petición POST a la API
response = requests.post(endpoint, headers=headers, json=request_data)
result = response.json()

print(result)
# Deberíamos ver en result el idioma detectado, e.g., "Spanish" con su puntuación.
```

✅ **En resumen**, la detección de idioma nos indica **en qué idioma está escrito un texto** y cuán seguro está el servicio de su respuesta. Esto permite, por ejemplo, redirigir un email al equipo adecuado según el idioma, o saludar al usuario en su idioma automáticamente.

🧠 **Preguntas de auto-test:**

1. ¿Qué información devuelve la API de **detección de idioma** por cada documento analizado?

   * A. El idioma detectado y una puntuación de confianza.
   * B. La traducción del texto al inglés.
   * C. La emoción (sentimiento) dominante en el texto.

2. ¿Cuál es el **máximo de caracteres** que se puede enviar en un solo documento para detectar idioma con Azure AI Language?

   * A. 1000 caracteres.
   * B. 5120 caracteres.
   * C. 10 000 caracteres.
  
<br><br><br>
## Extracción de frases clave

📌 **Concepto clave ➜** Identificación de las palabras o frases más **relevantes** de un texto, es decir, aquellas que capturan las ideas centrales.

La **extracción de frases clave** toma uno o varios documentos de texto y devuelve una lista de términos o frases importantes presentes en cada documento. En otras palabras, **resalta las ideas principales** del texto de forma automática. Esta funcionalidad examina el contenido y extrae palabras y combinaciones de palabras que representan el tema o concepto esencial de ese texto.

Usos típicos y ventajas:

* 📑 **Resúmenes automáticos:** obtener palabras clave te ayuda a entender de qué trata un documento largo sin leerlo completo.
* 🔍 **Búsqueda inteligente:** puedes indexar documentos por sus frases clave para facilitar búsquedas temáticas.
* 🎯 **Recomendaciones:** en sistemas de recomendación, las palabras clave permiten relacionar documentos por temas similares.

Como en otros análisis de texto de Azure:

* Puede procesar documentos de hasta **5120 caracteres** cada uno, y varios a la vez en lote.
* No requiere que entrenes un modelo; es una característica pre-entrenada lista para usar.

**Ejemplo de solicitud (REST JSON):** Supongamos que queremos obtener las frases clave de un enunciado. Construimos la petición indicando `"kind": "KeyPhraseExtraction"` y proporcionando el texto y su idioma (para mejor precisión, especificamos `"language": "es"` si es español, `"en"` si es inglés, etc.):

```json
{
  "kind": "KeyPhraseExtraction",
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "es",
        "text": "Text Analytics es parte de Azure AI"
      }
    ]
  }
}
```

**Ejemplo de respuesta (JSON):** La API devolverá las frases clave encontradas en el documento. Siguiendo el ejemplo anterior, la respuesta podría ser:

```json
{
  "id": "1",
  "keyPhrases": [
    "Text Analytics",
    "Azure AI"
  ]
}
```

Aquí vemos que el servicio identificó *“Text Analytics”* y *“Azure AI”* como las frases clave que resumen el contenido del texto dado. Son, efectivamente, los conceptos más importantes mencionados.

**Ejemplo de código en Python (usando `requests`):** Veamos cómo llamar a la extracción de frases clave mediante Python:

```python
import requests

endpoint = "<YOUR_ENDPOINT>/language/analyze-text?api-version=2022-10-01"
api_key = "<YOUR_KEY>"

request_data = {
    "kind": "KeyPhraseExtraction",
    "analysisInput": {
        "documents": [
            {
                "id": "1",
                "language": "es",
                "text": "Text Analytics es parte de Azure AI"
            }
        ]
    }
}
headers = {
    "Ocp-Apim-Subscription-Key": api_key,
    "Content-Type": "application/json"
}

response = requests.post(endpoint, headers=headers, json=request_data)
result = response.json()

print(result)
# El resultado debería incluir una lista de frases clave como ["Text Analytics", "Azure AI"].
```

✅ **En resumen**, la extracción de frases clave **automáticamente resume** un texto devolviendo las palabras o expresiones más significativas. Es una forma rápida de conocer de qué se habla en un documento sin leer todo el contenido.

🧠 **Preguntas de auto-test:**

1. ¿Qué produce la función de **extracción de frases clave** al analizar un documento?

   * A. Una lista de palabras y frases importantes que reflejan los temas centrales.
   * B. Un resumen escrito del documento en párrafos.
   * C. El idioma y la traducción del texto.

2. ¿Para cuál de estas tareas **sería útil** la extracción de frases clave?

   * A. Detectar si un email es spam.
   * B. Encontrar los temas principales en las reseñas de un producto.
   * C. Traducir un texto del español al inglés.

<br><br><br>
## Análisis de sentimientos (opiniones)

📌 **Concepto clave ➜** Determinar automáticamente el **tono emocional** de un texto: positivo, negativo o neutral (y detectar si hay sentimientos mezclados).

El **análisis de sentimientos** (también llamado análisis de opiniones) evalúa un texto para decidir si la actitud o emoción expresada es positiva, negativa o neutral. Básicamente, le da al texto un “termómetro emocional”. Esta funcionalidad es muy útil, por ejemplo, para:

* 📈 **Opiniones de clientes:** saber si una reseña o comentario sobre un producto, servicio, película, etc. es favorable (positiva) o crítica (negativa).
* 📨 **Priorizar atención al cliente:** en una bandeja de correos o mensajes en redes sociales, atender primero aquellos mensajes con sentimiento *negativo* (clientes insatisfechos) o muy *positivo* (oportunidades de testimonios), según convenga.

**¿Qué devuelve?** Por cada documento analizado, el servicio proporciona:

* Un **sentimiento general del documento** (positivo, negativo, neutral o incluso “mixto” si hay una combinación balanceada de frases positivas y negativas).
* El **sentimiento de cada oración** individual dentro del texto, para entender partes específicas del discurso.
* Para cada nivel (documento u oración) se incluyen **puntuaciones de confianza** para cada categoría de sentimiento. Por ejemplo, un texto puede venir con algo así como 90% positivo, 8% neutral, 2% negativo según lo que haya detectado.

📊 **Interpretando las puntuaciones:** Cada puntuación es un valor entre **0 y 1** (que puede pensarse como 0% a 100%). Cuanto más alto, más seguro está el modelo de que el texto pertenece a esa categoría. Por ejemplo, una **confianza de 0.95 en “positivo”** indica una alta probabilidad de que realmente sea positivo el tono. Si las puntuaciones están repartidas, puede haber ambigüedad. Si hay mezcla de frases positivas y negativas, el sistema podría marcar el documento global como **"mixto"**.

**Ejemplo de solicitud (REST JSON):** Vamos a analizar el sentimiento de una frase en español. Indicamos `"kind": "SentimentAnalysis"` y proporcionamos el texto con su idioma:

```json
{
  "kind": "SentimentAnalysis",
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "es",
        "text": "Gran hotel cerca de todo, volveremos sin duda."
      }
    ]
  }
}
```

Esta frase expresa una experiencia positiva (un cliente satisfecho con un hotel).

**Ejemplo de respuesta (JSON):** La respuesta de la API nos podría indicar:

```json
{
  "id": "1",
  "sentiment": "positive",
  "confidenceScores": {
    "positive": 0.98,
    "neutral": 0.01,
    "negative": 0.01
  },
  "sentences": [
    {
      "sentiment": "positive",
      "confidenceScores": {
        "positive": 0.98,
        "neutral": 0.01,
        "negative": 0.01
      },
      "offset": 0,
      "length": 53,
      "text": "Gran hotel cerca de todo, volveremos sin duda."
    }
  ]
}
```

En este caso, el servicio clasificó tanto la oración como el documento completo como **positivo**, con alta confianza (\~0.98 en positivo, prácticamente 98%). Vemos que incluso desglosa el resultado por oración (aquí solo había una oración).

* 🟢 **Positivo**: sentimiento favorable (ej. elogios, satisfacción).
* 🟡 **Neutral**: no se percibe emoción fuerte (ej. hechos, descripciones objetivas).
* 🔴 **Negativo**: sentimiento desfavorable (ej. quejas, insatisfacción).

*(Si hubiera mezcla significativa de frases positivas y negativas en un mismo texto, podría etiquetarse el sentimiento general como “mixto”).*

**Ejemplo de código en Python (usando `requests`):** Veamos cómo realizar esta llamada en Python para obtener el sentimiento:

```python
import requests

endpoint = "<YOUR_ENDPOINT>/language/analyze-text?api-version=2022-10-01"
api_key = "<YOUR_KEY>"

request_data = {
    "kind": "SentimentAnalysis",
    "analysisInput": {
        "documents": [
            {
                "id": "1",
                "language": "es",
                "text": "Gran hotel cerca de todo, volveremos sin duda."
            }
        ]
    }
}
headers = {
    "Ocp-Apim-Subscription-Key": api_key,
    "Content-Type": "application/json"
}

response = requests.post(endpoint, headers=headers, json=request_data)
result = response.json()

print(result)
# El resultado incluirá 'sentiment': 'positive' (u otro valor) con sus puntuaciones.
```

✅ **En resumen**, el análisis de sentimientos nos dice **si un texto transmite emociones positivas, negativas o neutras**, permitiendo cuantificar opiniones. Esto ayuda a las empresas y desarrolladores a medir automáticamente la satisfacción o insatisfacción expresada en grandes volúmenes de texto.

🧠 **Preguntas de auto-test:**

1. ¿Qué **categorías de sentimiento** identifica el servicio Azure AI Language en un texto?

   * A. Solo dos categorías: Bueno o Malo.
   * B. Tres categorías principales: Positivo, Negativo, Neutral (y “Mixto” si hay combinación).
   * C. Emociones específicas como Alegría, Tristeza, Enojo.

2. El análisis de opiniones del servicio de lenguaje devuelve una **puntuación de confianza**...

   * A. Para indicar qué tan seguro está el modelo de su evaluación de sentimiento.
   * B. Para mostrar cuántas personas estuvieron de acuerdo con esa opinión.
   * C. Para medir la longitud del texto analizado.

<br><br><br>
## Reconocimiento de entidades con nombre (NER)

📌 **Concepto clave ➜** Identificación de **entidades nombradas** en un texto, clasificándolas en categorías como personas, lugares, organizaciones, fechas, etc.

El **Reconocimiento de Entidades con Nombre** – conocido por las siglas NER (Named Entity Recognition) – consiste en detectar y categorizar automáticamente **nombres propios u otras entidades importantes** mencionadas dentro de un texto. El servicio analiza el texto y encuentra menciones a entidades, etiquetándolas con su tipo correspondiente.

**¿Qué se considera una entidad?** Son elementos concretos que tienen un significado definido, por ejemplo:

* 🧑 **Personas** (names of people),
* 🌎 **Lugares** (ciudades, países, ubicaciones geográficas),
* 🏢 **Organizaciones** (empresas, instituciones),
* 📅 **Fechas y horas** (tiempo: fechas, horas, días festivos),
* 📧 **Direcciones de correo**, 🏠 **direcciones postales**, 🔢 **números de teléfono**,
* 🌐 **URLs** (enlaces web),
* …entre otros.

*(El servicio de Azure AI Language tiene una lista amplia de categorías y subcategorías de entidad que puede reconocer; por ejemplo, dentro de “Dirección” distingue si es física o URL, dentro de “FechaHora” distingue fecha específica o rango, etc.)*

Por cada entidad detectada en el texto, la API devuelve detalles clave:

* **El texto exacto** de la entidad tal como aparece en el documento.
* **Categoría** asignada (por ej., Person, Location, Organization, DateTime, etc.) y a veces una **subcategoría** más específica (por ej., Location → GPE que indica Entidad geopolítica, como una ciudad/país).
* **Posición en el texto** (offset y length, es decir, en qué carácter del texto inicia y cuántos caracteres abarca la entidad reconocida).
* **Puntuación de confianza** (de 0 a 1) del modelo para esa identificación.

**Ejemplo de solicitud (REST JSON):** Supongamos el texto: *“Joe went to London on Saturday.”* (Joe fue a Londres el sábado). Queremos que la API identifique las entidades en esa frase en inglés:

```json
{
  "kind": "EntityRecognition",
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "Joe went to London on Saturday."
      }
    ]
  }
}
```

**Ejemplo de respuesta (JSON):** La respuesta indicaría las entidades encontradas y sus categorías. Para el texto dado, el resultado podría ser:

```json
{
  "id": "1",
  "entities": [
    {
      "text": "Joe",
      "category": "Person",
      "confidenceScore": 0.95
    },
    {
      "text": "London",
      "category": "Location",
      "subcategory": "GPE",
      "confidenceScore": 0.99
    },
    {
      "text": "Saturday",
      "category": "DateTime",
      "subcategory": "Date",
      "confidenceScore": 0.98
    }
  ]
}
```

En este caso, **“Joe”** fue reconocido como **Persona**, **“London”** como **Lugar** (subcategoría GPE indica que es una entidad geopolítica, es decir, una ciudad/país) y **“Saturday”** como **Fecha** (dentro de DateTime). Cada una con alta confianza (los valores son altos, cercanos a 1).

**Ejemplo de código en Python (usando `requests`):**

```python
import requests

endpoint = "<YOUR_ENDPOINT>/language/analyze-text?api-version=2022-10-01"
api_key = "<YOUR_KEY>"

request_data = {
    "kind": "EntityRecognition",
    "analysisInput": {
        "documents": [
            {
                "id": "1",
                "language": "en",
                "text": "Joe went to London on Saturday."
            }
        ]
    }
}
headers = {
    "Ocp-Apim-Subscription-Key": api_key,
    "Content-Type": "application/json"
}

response = requests.post(endpoint, headers=headers, json=request_data)
result = response.json()

print(result)
# El resultado listará entidades encontradas, por ejemplo Person, Location, DateTime con sus valores.
```

✅ **En resumen**, el reconocimiento de entidades permite **extraer información estructurada** de un texto no estructurado. Después de este análisis, sabrás qué **nombres propios, lugares, fechas u otros datos clave** aparecen en el texto, lo cual es muy útil para tareas como analizar documentos legales (encontrar nombres de partes, fechas de contratos), procesar noticias (listar personas u organizaciones mencionadas), o detectar datos personales sensibles (como correos o teléfonos, para enmascararlos si fuera necesario).

🧠 **Preguntas de auto-test:**

1. ¿Qué hace el **Reconocimiento de Entidades con Nombre (NER)** en un texto?

   * A. Clasifica cada palabra como correcta o incorrecta.
   * B. Identifica y clasifica entidades (personas, lugares, organizaciones, etc.) mencionadas.
   * C. Traduce los nombres propios a otro idioma.

2. ¿Cuál de los siguientes **NO** es un ejemplo de categoría de entidad que reconoce Azure AI Language?

   * A. Persona
   * B. Ubicación
   * C. Emoción del autor del texto
     
<br><br><br>
## Vinculación de entidades (Entity Linking)

📌 **Concepto clave ➜** **Desambiguación** de entidades mencionadas en un texto, conectándolas con referencias conocidas (por ejemplo, artículos de Wikipedia) para clarificar **de qué entidad específica se habla**.

La **vinculación de entidades** va un paso más allá del reconocimiento de entidades. Cuando una palabra puede referirse a más de una cosa, esta funcionalidad utiliza el contexto para **determinar exactamente a cuál entidad se refiere** y la enlaza con una fuente de información externa (actualmente, Wikipedia). En otras palabras, **desambigua** términos ambiguos.

¿Por qué es útil? Imagina que en un texto aparece “Venus”. ¿Se refiere al planeta Venus? ¿A la diosa romana Venus? ¿A una marca o personaje llamado así? La API de vinculación de entidades analizará las palabras alrededor (el contexto) para inferir la referencia correcta y te dará un enlace a la información relevante:

* 🔗 **Referencia de conocimiento:** Proporciona normalmente un URL a la página de Wikipedia correspondiente a la entidad. Wikipedia actúa como la base de conocimiento para aclarar de quién o qué estamos hablando.
* Si el texto no da suficiente contexto, la puntuación de confianza será baja o podría no vincular a nada específico.

**Ejemplo ilustrativo:**

* Input: *“Vi a Venus brillando en el cielo.”* → Lo más probable es que *Venus* se refiera al **planeta Venus**, y la API devolvería un link a la página de Wikipedia del planeta.
* Input: *“Venus, la diosa de la belleza, ...”* → Aquí *Venus* se refiere claramente a la **diosa romana**, y la API lo vincularía a la página de Wikipedia de Venus (mitología).

**Ejemplo de solicitud (REST JSON):** Analicemos la primera situación en inglés para mayor claridad. Indicamos `"kind": "EntityLinking"` con el texto:

```json
{
  "kind": "EntityLinking",
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "I saw Venus shining in the sky."
      }
    ]
  }
}
```

**Ejemplo de respuesta (JSON):** La respuesta identificaría *“Venus”* y la vincularía a la entidad correcta:

```json
{
  "id": "1",
  "entities": [
    {
      "name": "Venus",
      "matches": [
        {
          "text": "Venus",
          "offset": 6,
          "length": 5,
          "confidenceScore": 0.87
        }
      ],
      "language": "en",
      "id": "Venus",
      "url": "https://en.wikipedia.org/wiki/Venus",
      "dataSource": "Wikipedia"
    }
  ]
}
```

En este resultado:

* `"name": "Venus"` es la entidad detectada.
* Bajo `"matches"` se detalla dónde apareció ese texto en el documento (posición y longitud) y una puntuación de confianza sobre la coincidencia.
* Lo más importante: nos da la **URL** de Wikipedia que corresponde a la interpretación correcta de *Venus* en este contexto (en este caso, `wiki/Venus` que es el planeta).
* `"dataSource": "Wikipedia"` indica que la fuente de conocimiento utilizada es Wikipedia (por ahora, la única que emplea Azure para esta tarea).
* Un `"id"` interno (como `"Venus"`) puede aparecer, pero lo clave para el usuario es el nombre y el enlace.

**Ejemplo de código en Python (usando `requests`):**

```python
import requests

endpoint = "<YOUR_ENDPOINT>/language/analyze-text?api-version=2022-10-01"
api_key = "<YOUR_KEY>"

request_data = {
    "kind": "EntityLinking",
    "analysisInput": {
        "documents": [
            {
                "id": "1",
                "language": "en",
                "text": "I saw Venus shining in the sky."
            }
        ]
    }
}
headers = {
    "Ocp-Apim-Subscription-Key": api_key,
    "Content-Type": "application/json"
}

response = requests.post(endpoint, headers=headers, json=request_data)
result = response.json()

print(result)
# Deberíamos obtener la entidad "Venus" con un enlace a Wikipedia en result.
```

✅ **En resumen**, la vinculación de entidades **identifica correctamente de qué entidad se habla y la enlaza con información adicional** (usualmente Wikipedia). Es ideal para enriquecer texto con datos externos, crear enlaces automáticos en documentos o simplemente entender mejor a qué se refiere un término dentro de un contexto. Por ejemplo, en análisis de texto a gran escala podríamos automáticamente obtener referencias de todos los personajes, lugares o conceptos mencionados en un artículo.

🧠 **Preguntas de auto-test:**

1. ¿Qué problema resuelve la **vinculación de entidades** en el procesamiento de texto?

   * A. Traduce automáticamente los nombres propios al español.
   * B. Diferencia entre entidades ambiguas y determina a cuál se refiere, enlazándola a una fuente como Wikipedia.
   * C. Convierte las frases clave en etiquetas HTML.

2. ¿Cuál es la **principal fuente de información** que utiliza Azure AI Language para vincular entidades actualmente?

   * A. Una base de datos local proporcionada por el usuario.
   * B. Google Search.
   * C. Wikipedia.

<br><br><br>
## Glosario de términos clave

* **Procesamiento de Lenguaje Natural (PLN/NLP):** Campo de la inteligencia artificial que se enfoca en que las máquinas **entiendan y procesen el lenguaje humano** (texto o voz). *Ejemplo:* interpretar el significado de una frase escrita.
* **Azure AI Language:** Servicio en la nube de Azure que ofrece múltiples funcionalidades de NLP **pre-entrenadas** (listas para usar) y **personalizables**, como las descritas en este resumen, a través de APIs y SDKs.
* **Endpoint (Punto de conexión):** URL única proporcionada por Azure cuando creas el servicio, a la cual tu aplicación debe enviar las peticiones. *Es como la “dirección web” de tu servicio de lenguaje en Azure.*
* **Clave de suscripción (API Key):** Contraseña secreta (cadena de caracteres) que Azure te da para **autenticar tus solicitudes** a la API. Se incluye en las cabeceras de cada petición para demostrar que tienes permiso de usar el servicio.
* **API REST:** Interfaz de programación basada en **peticiones HTTP** (normalmente JSON) para comunicarse con servicios web. Azure AI Language ofrece una API REST, lo que significa que puedes enviar datos (texto) mediante una solicitud HTTP POST y recibir la respuesta (análisis) en formato JSON.
* **SDK:** *Software Development Kit* – Conjunto de herramientas/proporcionado por Azure para distintos lenguajes de programación (Python, C#, Java, etc.) que facilita el uso de la API. En lugar de construir manualmente las peticiones HTTP, puedes llamar a funciones del SDK que internamente ya manejan esas peticiones.
* **JSON:** *JavaScript Object Notation* – Formato ligero de texto para **enviar y recibir datos estructurados**. Las APIs de Azure devuelven los resultados en JSON (llaves y valores), como hemos visto en los ejemplos.
* **Detección de idioma:** Funcionalidad que **identifica el idioma** de un texto y proporciona una puntuación de confianza. *Por ejemplo, dado “Hello”, determina que está en Inglés (en) con alta seguridad.*
* **Análisis de sentimientos:** Funcionalidad que **determina la actitud** o tono emocional de un texto (positivo, neutral, negativo) con puntuaciones de confianza. *Por ejemplo, “Me encanta este producto” → Positivo.*
* **Frase clave:** Palabra o grupo de palabras que **resume un tema importante** en el texto. La extracción de frases clave devuelve estas palabras importantes. *Ejemplo: de “El gato está sobre la alfombra roja”, podría extraer “gato” y “alfombra roja”.*
* **Entidad con nombre:** Un **elemento del mundo real mencionado en un texto**, categorizado por tipo. Puede ser una persona, lugar, organización, fecha, etc. *Ej.: “Madrid” es una entidad de tipo Lugar (ciudad).*
* **Vinculación de entidades:** Proceso de **conectar una entidad mencionada con su referencia en una base de conocimiento** para eliminar ambigüedades. *Ej.: vincular “Mercurio” a Mercury (planeta) vs Mercury (elemento químico) según contexto, generalmente usando Wikipedia.*
* **Puntuación de confianza:** Un número entre 0 y 1 que indica **qué tan seguro está el modelo** de su resultado. Un valor cercano a 1 (ej. 0.98) significa muy alta confianza; cercano a 0 significa baja confianza.
* **Información de Identificación Personal (PII):** Datos sensibles que pueden identificar a una persona (nombre completo, teléfono, email, número de tarjeta, etc.). Azure AI Language tiene funcionalidad para **detectar y enmascarar PII** en texto, protegiendo la privacidad.
* **Resumen (Sumarización):** Funcionalidad que **sintetiza un texto largo en uno más corto**, extrayendo oraciones clave o generando un párrafo resumido. Ayuda a obtener la idea general sin leer todo el contenido original.

<br><br><br>
## Tabla resumen (Flashcards)

A continuación, se presenta una tabla a modo de *flashcards* para repasar rápidamente cada servicio y su propósito principal, junto con una palabra clave que ayude a recordarlo:

| **Servicio de Azure AI Language**     | **Función principal**                     | **Palabra clave** |
| ------------------------------------- | ----------------------------------------- | ----------------- |
| **Detección de idioma**               | Identifica el idioma de un texto          | Idioma            |
| **Análisis de sentimientos**          | Determina tono: positivo/negativo/neutral | Sentimiento       |
| **Extracción de frases clave**        | Extrae términos importantes (ideas clave) | Ideas             |
| **Reconocimiento de entidades (NER)** | Encuentra y clasifica entidades nombradas | Entidades         |
| **Vinculación de entidades**          | Desambigua entidades y las enlaza a info  | Wikipedia         |
| **Detección de PII**                  | Detecta datos personales sensibles        | Privacidad        |
| **Resumen (Sumarización)**            | Resume textos largos en breves oraciones  | Resumen           |

Cada fila de la tabla resume un **servicio de lenguaje** de Azure:

* En la primera columna está el **nombre de la funcionalidad**.
* En la segunda, su **propósito principal** en pocas palabras.
* En la tercera, una **palabra clave** para recordar de qué se trata (por ejemplo, vinculación de entidades ⇒ pensar en *Wikipedia*, ya que enlaza con ella).
