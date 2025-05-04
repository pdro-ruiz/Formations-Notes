# Creación de soluciones de Computer Vision en Azure

## Azure AI Vision

> 📌 **Concepto clave ➜** Azure AI Vision es un servicio de visión por computadora en Azure que permite analizar imágenes automáticamente (etiquetado, detección de objetos/personas, lectura de texto, etc.).

Azure AI Vision ofrece **capacidades preentrenadas** que se pueden integrar fácilmente en apps. Entre sus funciones destacan: generación automática de títulos y etiquetas, detección de objetos y personas con sus *bounding boxes*, análisis de metadatos visuales (formato, colores, puntos de referencia), categorización temática, eliminación de fondo, moderación de contenido (vídeos o imágenes con violencia o desnudos), OCR para extraer texto de imágenes y generación de **miniaturas inteligentes** (recortes óptimos). Por ejemplo, con una sola llamada se puede analizar una imagen y obtener las etiquetas o el texto extraído.

* 💡 **Aprovisionamiento:** Azure AI Vision puede crearse como recurso individual o como parte de un recurso multiservicio de Azure AI Services.
* ⚠️ **Atención:** Para usar funcionalidades avanzadas (reconocimiento de celebridades o monumentos) se debe solicitar acceso limitado.
* ✅ **Respuesta:** El servicio devuelve un objeto JSON estructurado con los resultados solicitados.

**Ejemplo práctico (Python):** Análisis de imagen con título y OCR.

```python
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.vision.imageanalysis.models import VisualFeatures
from azure.core.credentials import AzureKeyCredential

client = ImageAnalysisClient(
    endpoint=os.environ["ENDPOINT"],
    credential=AzureKeyCredential(os.environ["KEY"])
)
result = client.analyze(
    image_url="https://example.com/image.jpg",
    visual_features=[
        VisualFeatures.CAPTION,  # Genera un subtítulo automático
        VisualFeatures.READ      # Realiza OCR (reconoce texto)
    ],
    gender_neutral_caption=True,
    language="en"
)
print(result.caption)  # Título descriptivo de la imagen
```

Este código usa el SDK de Azure AI Vision para analizar una imagen, solicitando la generación de un *caption* y la lectura de texto. En resumen, **para analizar imágenes** se puede usar la API REST (Analyze Image) o los SDK oficiales.

#### Preguntas de autoevaluación

* ¿Qué capacidades incluye Azure AI Vision y cómo se accede a ellas?
* ¿Cuál es la diferencia entre Azure AI Vision y Azure Face?
* ¿Qué formato tiene la respuesta al analizar una imagen con Azure AI Vision?

<br><br><br>
## Generación de miniaturas inteligentes y eliminación de fondo

> 📌 **Concepto clave ➜** *Miniaturas inteligentes* recortan automáticamente la región más relevante de una imagen para mostrarla como vista previa; *eliminación de fondo* separa el sujeto principal del fondo creando una máscara alfa.

Estas funciones mejoran la presentación y edición de imágenes:

* **Miniaturas inteligentes (Smart Crops):** Crea una versión reducida de la imagen centrada en el elemento más importante. Sirve para vistas previas atractivas en catálogos o webs, sin recortar manualmente cada imagen. Se especifica el ancho y alto deseado y se activa el recorte inteligente (relaciones de aspecto de 0.75 a 1.80).

* **Eliminación de fondo:** Azure AI Vision genera una *máscara alfa* que distingue el primer plano del fondo. A partir de la máscara se puede obtener el sujeto sin fondo (por ejemplo, un PNG con transparencia) y/o el fondo por separado. Esto es útil para crear imágenes sin fondo, mejorar recortes automáticos en e-commerce o integraciones de diseño.

> 💡 *Tip:* Ambas funcionalidades se activan usando las características visuales **SMART\_CROPS** y **REMOVED\_BACKGROUND** en el análisis de imagen (VisualFeatures.SMART\_CROPS, VisualFeatures.OBJECT, etc.). Por ejemplo, con el SDK se puede solicitar Smart Crops junto con otros análisis.

#### Preguntas de autoevaluación

* ¿Para qué sirve la función de miniaturas inteligentes y qué parámetros clave la controlan?
* ¿Cómo obtiene Azure AI Vision la máscara alfa al eliminar el fondo?
* Menciona tres casos de uso típicos de la eliminación de fondo.

<br><br><br>
## Clasificación de imágenes con Custom Vision

> 📌 **Concepto clave ➜** *Custom Vision* permite entrenar modelos personalizados de clasificación de imágenes, asignando etiquetas a objetos o escenas definidas por el usuario.

La **clasificación de imágenes** consiste en asignar una imagen completa a una categoría. En Azure se usa el servicio **Custom Vision** para crear estos modelos desde cero. Para entrenar, se necesitan dos recursos de Azure:

1. Un recurso de entrenamiento (Custom Vision Training) donde se suben y etiquetan las imágenes.
2. Un recurso de predicción (Custom Vision Prediction) donde se publica el modelo entrenado para uso en la aplicación cliente. Ambos pueden ser un recurso dedicado o parte del recurso multiservicio.

El flujo básico es:

1. **Entrenamiento:** Subir muchas imágenes etiquetadas por clase.
2. **Publicación:** Publicar el modelo en el recurso de predicción.
3. **Consumo:** Enviar nuevas imágenes al modelo para obtener etiquetas en tiempo real o por lotes.

> 💡 *Importante:* Cuantas más imágenes por categoría (etiqueta), mejor la precisión del modelo.

#### Preguntas de autoevaluación

* ¿Qué es Custom Vision y para qué se usa?
* ¿Qué recursos de Azure son necesarios para entrenar y publicar un modelo de clasificación?
* Describe brevemente las etapas de entrenamiento y consumo de un modelo de clasificación.

<br><br><br>
## Detección de objetos

> 📌 **Concepto clave ➜** La *detección de objetos* identifica múltiples objetos en una imagen y devuelve un *bounding box* con coordenadas para cada uno.

A diferencia de la clasificación (una sola etiqueta para toda la imagen), la detección localiza cada objeto con una etiqueta y un rectángulo delimitador. Cada predicción de objeto incluye: la etiqueta de la clase (qué es el objeto) y la ubicación (coordenadas del bounding box).

Para entrenar un detector con Custom Vision:

* Se requieren dos recursos en Azure (entrenamiento y predicción).
* En el portal de Custom Vision se suben imágenes y se dibujan rectángulos delimitadores indicando cada objeto.
* Las herramientas soportan el etiquetado manual o semiautomático (etiquetador inteligente). También hay herramientas externas (Azure ML Studio, VoTT) para etiquetar en colaboración.
* Los bounding boxes se definen con coordenadas relativas (izquierda, superior, ancho, alto) en decimal respecto a la imagen.

> ⚠️ *Nota:* Asegúrate de definir correctamente los rectángulos (porcentajes) al exportar o usar la API; son cruciales para que el modelo entienda la ubicación.

#### Preguntas de autoevaluación

* ¿Qué diferencia existe entre clasificación de imágenes y detección de objetos?
* ¿Qué datos incluye la predicción de un objeto detectado?
* ¿Cómo se representan los *bounding boxes* en Custom Vision?

<br><br><br>
## Detección y análisis de rostros

> 📌 **Concepto clave ➜** Azure AI Vision puede detectar personas en imágenes (con bounding boxes), mientras que **Azure Face** es un servicio especializado que ofrece detección avanzada y reconocimiento facial.

**Azure AI Vision (generalista):** Con VisualFeatures.PEOPLE, detecta personas devolviendo coordenadas y nivel de confianza. Sirve para contar personas o análisis de presencia, pero no brinda detalles faciales (edad/género han sido retirados por diseño responsable).

**Azure Face (especializado):** Ofrece detección de caras (bounding box), análisis detallado (posición de cabeza, emociones, gafas, puntos clave…) y funciones de comparación y reconocimiento de identidad. Para usar verificación o identificación de personas únicas se requiere **acceso limitado**. Azure Face incluye:

* **Detección de caras:** Retorna un ID único para cada cara detectada y su bounding box.
* **Análisis de rasgos:** Indica atributos como rotación de cabeza 3D, uso de accesorios (gafas, gorro), calidad para reconocimiento (bajo/alto), coordenadas clave (ojos, nariz…).
* **Comparación de caras:** Determina si dos imágenes corresponden a la misma persona.
* **Reconocimiento facial:** Identifica o verifica una cara contra un grupo entrenado de personas (PersonGroup).
* **Detección de vivacidad:** Comprueba si la imagen proviene de una fuente real (vídeo en vivo) para prevenir suplantaciones.

> ⚠️ *Responsabilidad:* El tratamiento de datos faciales es sensible (identificadores biométricos). Debe considerarse privacidad (cumplir GDPR), transparencia (informar al usuario) y equidad (datos diversos para evitar sesgos). Por ética, Azure Face ya no predice edad o género del sujeto.

#### Preguntas de autoevaluación

* ¿Cómo difiere Azure AI Vision de Azure Face en el manejo de imágenes con personas?
* ¿Qué información ofrece el análisis de rasgos faciales de Azure Face?
* ¿Qué pasos implica entrenar un modelo de reconocimiento facial con Azure Face?

<br><br><br>
## OCR: Leer texto en imágenes

> 📌 **Concepto clave ➜** El OCR (Reconocimiento Óptico de Caracteres) con Azure AI Vision *Read API* extrae texto de imágenes (señales, documentos, recibos) de forma automática.

Azure AI Vision incluye la característica **READ** para leer texto de imágenes. Es una operación síncrona que devuelve en una sola llamada cadenas de texto extraídas, organizadas en bloques, líneas y palabras. El servicio compara varios casos de uso (señales, notas, carteles) y puede manejar documentos impresos o manuscritos.

Para usarlo:

* Se invoca `client.analyze` con la característica `VisualFeatures.READ`.
* En la llamada REST se usa el endpoint `imageanalysis:analyze?features=Read` con la URL o bytes de la imagen.

**Ejemplo (Python):**

```python
result = client.analyze(
    image_url="https://example.com/receipt.jpg",
    visual_features=[VisualFeatures.READ]
)
```

Este código devuelve en `result` un objeto que contiene el texto reconocido en formato estructurado.

**Ejemplo (REST curl):**

```bash
curl -X POST "https://<endpoint>/computervision/imageanalysis:analyze?features=Read&language=en" \
  -H "Ocp-Apim-Subscription-Key: <tu_clave>" \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com/image.jpg"}'
```

El resultado JSON incluye jerarquía: **Bloques → Líneas → Palabras**, cada palabra con su texto, posición (polígono) y confianza.

#### Preguntas de autoevaluación

* ¿Qué estructura sigue la respuesta del OCR en Azure AI Vision?
* ¿Cómo se solicita el servicio de OCR usando Python y usando REST?
* ¿Para qué casos es más adecuado usar OCR y qué alternativa de Azure existe para documentos complejos?

<br><br><br>
## Azure Video Indexer

> 📌 **Concepto clave ➜** *Azure Video Indexer* es un servicio que extrae insights avanzados de archivos de video (etiquetas, personajes, transcripción, etc.) de forma automática.

Este servicio analiza vídeos completos y proporciona metadatos útiles: detección facial (personas en pantalla, requiere acceso limitado), OCR en video, transcripción de audio con identificación de locutores, análisis de temas y sentimientos, etiquetas de objetos o acciones, moderación de contenido y segmentación por escenas. Todo se puede manejar desde el portal de Video Indexer o mediante API.

Entre sus opciones avanzadas está la creación de modelos personalizados para: reconocimiento facial específico, vocabulario especializado (mejorar transcripción de jerga), identificación de marcas o logos personalizados. También ofrece **widgets** incrustables para mostrar análisis de vídeo en tus propias aplicaciones.

**Integración mediante API REST:**

* Se obtiene un token de acceso con una llamada GET al endpoint de autenticación:

```bash
curl -X GET "https://api.videoindexer.ai/Auth/<ubicación>/Accounts/<accountId>/AccessToken?allowEdit=true" \
  -H "Ocp-Apim-Subscription-Key: <tu_clave>"
```

* Con ese token se puede, por ejemplo, listar los videos de la cuenta:

```bash
curl -X GET "https://api.videoindexer.ai/<ubicación>/Accounts/<accountId>/Videos?accessToken=<token>"
```

Esta API permite automatizar tareas como subir vídeos, iniciar análisis, consultar resultados y gestionar personalizaciones (logos, nombres propios, etc.).

#### Preguntas de autoevaluación

* ¿Qué funcionalidades generales ofrece Azure Video Indexer? Menciona al menos tres.
* ¿Cómo obtienes un token de acceso para usar la API de Video Indexer?
* ¿Para qué sirven los widgets de Video Indexer?

<br><br><br>
## IA Generativa con Visión

> 📌 **Concepto clave ➜** Los modelos multimodales (texto + imagen) de Azure AI Foundry permiten crear aplicaciones conversacionales que entienden imágenes y texto simultáneamente.

Con Azure AI Foundry se pueden implementar chatbots que procesen entrada visual. Modelos como **Phi-4-multimodal** u **OpenAI GPT-4o** admiten prompts que combinan texto e imágenes. En el Azure Portal existe un área de pruebas donde se puede:

* Subir una imagen y escribir texto en el prompt.
* Obtener una respuesta donde el modelo interpreta ambos.

Para integrar esto en una app:
Se envía una solicitud al endpoint del modelo con un JSON que incluya mensajes con tipo texto e imagen. Por ejemplo:

```json
{
  "messages": [
    {"role": "system", "content": "Eres un asistente útil."},
    {
      "role": "user",
      "content": [
        {"type": "text", "text": "Describe esta imagen:"},
        {"type": "image_url", "image_url": {"url": "https://example.com/foto.jpg"}}
      ]
    }
  ]
}
```

En respuesta, el modelo usa tanto el contenido visual como textual para generar su respuesta. Se puede acceder al modelo mediante la API de OpenAI o el cliente de Azure AI, usando SDKs como Python.

#### Preguntas de autoevaluación

* ¿Qué es un modelo multimodal y cómo se usa en Azure AI Foundry?
* ¿Qué contiene el JSON enviado a un modelo multimodal para interpretar texto e imagen?
* Nombra dos modelos compatibles con Azure AI Foundry para entrada visual.

<br><br><br>
## Generación de imágenes con Azure OpenAI (DALL·E)

> 📌 **Concepto clave ➜** *DALL·E* es un modelo de Azure OpenAI que genera imágenes originales a partir de descripciones en texto.

El servicio Azure OpenAI permite generar gráficos con lenguaje natural. DALL·E crea nuevas imágenes (no sólo busca existencias) basándose en el prompt textual. Por ejemplo, el texto “Una ardilla en una motocicleta” produce una imagen única acorde a esa descripción.

**Cómo usarlo:** Desde Azure OpenAI (p.ej. Azure AI Studio) se puede ajustar resolución (p.ej. 1024×1024), estilo (vivid o natural) y calidad. Mediante la API REST se envía una solicitud POST con JSON que incluye:

* `prompt`: descripción en texto.
* `n`: número de imágenes (DALL·E 3 solo admite n=1).
* `size`: resolución.
* Opcionales: `quality` (“standard” o “hd”), `style` (“vivid” o “natural”).

```json
{
  "prompt": "Un tejón con esmoquin",
  "n": 1,
  "size": "1024x1024",
  "quality": "hd",
  "style": "vivid"
}
```

La respuesta es síncrona y devuelve la URL de la imagen generada. Por ejemplo:

```json
{
  "created": 1686780744,
  "data": [
    {
      "url": "https://...imagen_generada.png",
      "revised_prompt": "A well-dressed badger in a tuxedo"
    }
  ]
}
```

Donde `url` es la dirección directa de la imagen PNG y `revised_prompt` muestra cómo DALL·E ajustó el texto interno.

#### Preguntas de autoevaluación

* ¿Qué parámetros clave se envían a la API de DALL·E para generar una imagen?
* ¿Qué es `revised_prompt` en la respuesta de DALL·E?
* Menciona un caso de uso práctico para la generación de imágenes con IA.

<br><br><br>
## Glosario

* **Azure AI Vision:** Servicios de visión artificial en Azure para análisis de imágenes (detección, OCR, descripciones, etc.).
* **Custom Vision:** Servicio de Azure para entrenar y publicar modelos personalizados de clasificación de imágenes.
* **Azure Face:** Servicio especializado en detección, análisis y reconocimiento facial con capacidades biométricas.
* **Azure Video Indexer:** Servicio de análisis de vídeo que extrae etiquetas, rostros, texto, transcripciones y más de grabaciones multimedia.
* **Smart Crops (miniaturas inteligentes):** Función de recorte inteligente de Azure AI Vision que genera miniaturas centradas en el sujeto más relevante.
* **Máscara alfa:** Imagen en escala de grises que separa primer plano y fondo, usada en eliminación de fondo.
* **Bounding Box:** Rectángulo delimitador que rodea un objeto o rostro detectado, definido por coordenadas relativas.
* **OCR (Read API):** Característica de Azure AI Vision para extraer texto de imágenes y documentos.
* **PersonGroup:** Agrupación en Azure Face donde se añaden múltiples imágenes de un mismo individuo para entrenamiento de reconocimiento facial.
* **Vídeo Indexer Token:** Token de autenticación obtenido mediante API para usar Azure Video Indexer.
* **Multimodal:** Modelos que procesan simultáneamente texto e imagen como entrada (Azure AI Foundry).
* **DALL·E:** Modelo generativo de Azure OpenAI que crea imágenes originales a partir de un texto descriptivo.
* **Prompt:** Texto de entrada usado para guiar al modelo generativo (visión o lenguaje natural).
* **Humano:** Participante del chat o del sistema que provee texto o imagen para el modelo.
* **API REST:** Interfaz de Azure que permite consumir los servicios de Vision y OpenAI mediante HTTP.

<br><br><br>
## Tarjetas de repaso (Flashcards)

| Servicio o Funcionalidad    | Descripción breve                                                                                    | Palabra clave |
| --------------------------- | ---------------------------------------------------------------------------------------------------- | ------------- |
| **Azure AI Vision**         | Servicio de visión computacional pre-entrenado de Azure (análisis de imágenes: detección, OCR, etc.) | Vision        |
| **Custom Vision**           | Plataforma para entrenar modelos de clasificación de imágenes con datos propios                      | Clasificación |
| **Azure Face**              | Servicio especializado en detección y reconocimiento facial con funciones avanzadas                  | Face          |
| **Azure Video Indexer**     | Servicio para analizar vídeos y extraer información (rostros, texto, transcripción, etc.)            | Vídeo         |
| **Miniaturas inteligentes** | Función de Azure Vision para recortar imágenes enfocando en el elemento principal                    | Miniaturas    |
| **Eliminación de fondo**    | Función que separa el sujeto del fondo usando una máscara alfa                                       | Transparencia |
| **OCR (Read API)**          | Característica que extrae texto de imágenes o vídeos usando Azure AI Vision                          | OCR           |
| **Bounding Box**            | Rectángulo con coordenadas que encierra un objeto o rostro detectado                                 | Caja          |
| **Azure AI Foundry**        | Plataforma de modelos multimodales (texto+imagen) para crear chatbots inteligentes                   | Multimodal    |
| **DALL·E (Azure OpenAI)**   | Modelo de generación de imágenes a partir de texto en Azure OpenAI Service                           | DALL·E        |
