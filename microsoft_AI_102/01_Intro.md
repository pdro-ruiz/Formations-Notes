# Introducción a Servicios de Azure AI

## ¿Qué es la inteligencia artificial?

> 📌 **Concepto clave ➜** Inteligencia Artificial (IA) es la capacidad de un software de **imitar el comportamiento humano** en tareas que normalmente requieren inteligencia.

La IA abarca múltiples **capacidades similares a las humanas** que permiten desarrollar aplicaciones inteligentes. Entre las áreas principales de la IA se incluyen:

* **IA generativa:** capacidad de **generar contenido original** (texto, imágenes, código, etc.) a partir de indicaciones en lenguaje natural (por ejemplo, modelos GPT que crean respuestas únicas).
* **Agentes autónomos:** aplicaciones de IA generativa (bots o asistentes) que **responden autónomamente** a entradas del usuario o situaciones y toman acciones apropiadas.
* **Visión por computadora:** capacidad de **interpretar imágenes y videos**, identificando objetos, personas o escenarios en contenido visual.
* **Voz (Speech):** capacidad de **reconocer habla y sintetizar voz**, incluyendo convertir voz a texto, texto a voz, reconocer quién habla e incluso traducir oralmente.
* **Procesamiento de lenguaje natural (NLP):** capacidad de **entender y generar lenguaje humano** escrito o hablado; por ejemplo, analizando texto para extraer ideas clave, sentimientos o resúmenes.
* **Extracción de información:** combina visión, voz y lenguaje para **extraer datos clave** de documentos, formularios, imágenes, grabaciones u otros contenidos (ej: extraer campos de una factura).
* **Soporte de decisiones:** capacidad de usar datos históricos y **modelos predictivos** para apoyar decisiones (ej: predicciones de demanda, detección de anomalías para mantenimiento).

Estas áreas se complementan entre sí y muchas soluciones de IA integran varias de ellas. En resumen, la IA permite a las aplicaciones **aprender de los datos y experiencias** para realizar tareas complejas de forma más similar a como lo haría un humano.

**💡 Importante:** Aunque la IA puede facilitar tareas, **suele trabajar con modelos probabilísticos**, no deterministas. Esto significa que sus respuestas pueden variar y no siempre serán perfectas; por ello es crucial entender sus capacidades y limitaciones.

**Preguntas de autoevaluación:**

1. ¿Cuál de las siguientes opciones **NO** corresponde a una rama o capacidad de la IA?
   a. Visión por computadora
   b. Generación de lenguaje natural
   c. Programación tradicional de bases de datos

2. Un agente conversacional que responde automáticamente a solicitudes de los usuarios y toma acciones se considera:
   a. Un ejemplo de IA generativa
   b. Un ejemplo de agente de IA autónomo
   c. Un sistema de soporte de decisiones

3. **Verdadero o Falso:** La IA generativa puede crear contenido original (como texto o imágenes) que no estaba previamente almacenado tal cual en sus datos de entrenamiento.

<br><br><br>
## Servicios de Azure AI

> 📌 **Concepto clave ➜** Los **Servicios de Azure AI** son un conjunto de servicios en la nube que brindan funcionalidades de IA **preconstruidas** para integrarlas fácilmente en tus aplicaciones.

Microsoft Azure ofrece una amplia gama de servicios de IA en la nube, que actúan como **bloques de construcción** inteligentes listos para usar. Estos servicios permiten incorporar visión artificial, comprensión del lenguaje, reconocimiento de voz y más, sin tener que crear modelos desde cero. A continuación se listan los servicios principales de Azure AI y su propósito:

* 🤖 **Azure OpenAI:** Proporciona acceso a **modelos de IA generativa** de OpenAI (como la familia GPT-3.5/4 y DALL-E). Permite generar texto, código o imágenes a partir de indicaciones. *Palabra clave: modelos GPT generativos*.
* 🖼️ **Visión de Azure AI:** APIs y modelos para tareas clásicas de **Computer Vision**. Permite detectar **objetos en imágenes**, generar **descripciones o etiquetas** automáticamente sobre el contenido visual, y realizar **lectura de texto en imágenes** (OCR).
* 🔊 **Voz de Azure AI:** APIs para integrar funciones de voz. Incluye **texto a voz** (sintetizar habla a partir de texto), **voz a texto** (transcribir audio hablado a texto), además de funciones avanzadas como **reconocimiento de hablantes** (identificar quién habla) y **traducción de voz** en tiempo real.
* 📖 **Lenguaje de Azure AI:** Modelos y APIs para **analizar texto en lenguaje natural**. Permite realizar **análisis de sentimientos**, **extracción de entidades (entidades nombradas, PII)**, **detección de idioma**, **resumen automático** de documentos, entre otras tareas de NLP.
* 🛡️ **Seguridad de contenido de Azure AI:** Servicio diseñado para **detectar y moderar contenido potencialmente ofensivo o riesgoso** en imágenes y texto. Emplea algoritmos avanzados para marcar contenidos de violencia, odio, sexual o autolesivo. *Se profundiza en este servicio en secciones posteriores.*
* 🌐 **Traductor de Azure AI:** Utiliza modelos de lenguaje de última generación para **traducir texto entre múltiples idiomas** de forma instantánea. Soporta decenas de idiomas, permitiendo traducciones precisas y contextuales.
* 🙂 **Azure AI Face:** Servicio de visión especializado en **detección, análisis y reconocimiento de rostros humanos** en imágenes. Puede identificar características faciales, estimar edad/emoción o comparar rostros. *⚠️ Debido a riesgos de privacidad, ciertas funciones avanzadas (por ejemplo, identificar personas) están restringidas a clientes aprobados.*
* 🎨 **Azure AI Custom Vision:** Permite **entrenar modelos de visión por computadora personalizados**. Ideal para crear tu propio clasificador de imágenes o detector de objetos específico, subiendo ejemplos etiquetados. Ofrece flexibilidad para casos donde los modelos genéricos de Vision no bastan.
* 📑 **Inteligencia de Documentos de Azure AI:** Combina visión y lenguaje para **extraer información de documentos estructurados o semiestructurados**. Incluye modelos predefinidos (por ejemplo, para extraer campos de facturas, recibos, identificaciones) y la opción de entrenar modelos custom con tus propios formularios. Es un **OCR avanzado** que no solo lee texto, sino que lo interpreta con significado (campos, tablas, etc.).
* 🔎 **Descripción del contenido de Azure AI:** *(Azure AI Content Understanding, vista previa)* Proporciona análisis de contenido **multimodal**. Permite crear modelos que **procesan documentos, imágenes, videos y audio** para extraer datos y insights combinando esas fuentes. Por ejemplo, podría indexar un video identificando objetos visuales, transcribiendo diálogo y extrayendo información clave, todo integrado. *Usa técnicas de IA generativa para comprender contenido en cualquier formato.*
* 🗂️ **Azure AI Search:** Servicio de búsqueda inteligente potenciado con IA. Usa **canalizaciones de habilidades cognitivas** (combinando varios servicios Azure AI y lógica personalizada) para **extraer información de contenido** (texto, documentos, etc.) y construir un índice de búsqueda enriquecido. Azure AI Search soporta crear **búsquedas semánticas y vectoriales**: esto es clave para soluciones con IA generativa, donde se crean índices vectoriales de documentos que luego sirven para “fundamentar” respuestas de modelos de lenguaje (por ejemplo, proporcionar contexto a GPT a partir de datos propios).

Cada uno de estos servicios se aprovisiona en Azure y expone funcionalidades mediante APIs o SDK. Puedes usarlos individualmente o combinarlos para construir soluciones más complejas (por ejemplo, un bot que use **Visión** para analizar una imagen y luego **Lenguaje** para describirla en texto, usando **Traductor** para varios idiomas).

**⚠️ Nota:** La mayoría de estos servicios de Azure AI se pueden crear de forma independiente, y muchos **incluyen un nivel gratuito** limitado. Esto permite probar y desarrollar con ellos sin incurrir en costos inicialmente (por ejemplo, ciertas cantidades de transacciones al mes sin cargo).

**Preguntas de autoevaluación:**

1. ¿Qué servicio de Azure AI usarías para *clasificar imágenes de productos en categorías específicas definidas por ti*?
   a. Azure AI Vision (genérico)
   b. Azure AI Custom Vision
   c. Azure AI Content Safety

2. **Verdadero o Falso:** Azure AI Search puede crear índices **vectoriales** de tus datos para mejorar búsquedas semánticas y brindar contexto a modelos generativos (LLM).

3. Un cliente quiere transcribir llamadas telefónicas y luego analizar el sentimiento de cada transcripción. ¿Qué combinación de servicios Azure AI es la más adecuada?
   a. Voz de Azure AI + Lenguaje de Azure AI
   b. Azure AI OpenAI + Azure AI Search
   c. Visión de Azure AI + Azure AI Custom Vision
   
<br><br><br>
## Consideraciones para los recursos de Azure AI

> 📌 **Concepto clave ➜** Un **recurso de Azure AI** es una instancia en la nube de un servicio de IA. Al crearlo debes elegir el tipo correcto, la región adecuada y planificar costos y seguridad.

Antes de usar cualquier servicio de Azure AI, necesitas **aprovisionar un recurso** en tu suscripción Azure. Este recurso representa al servicio (por ejemplo, un recurso de *Azure AI Language* para usar análisis de texto) y te proporcionará un **punto de conexión (endpoint URL)** y **claves de autenticación** para consumirlo. Al planificar la creación de recursos de Azure AI, ten en cuenta:

* **Tipo de recurso – servicio único vs. multiservicio:** La mayoría de servicios de Azure AI se pueden crear como **recursos independientes**, es decir, uno por servicio (ej: un recurso de *AI Language*, otro de *AI Vision*, etc.). Alternativamente, Azure ofrece un **recurso “Servicios de Azure AI” multiservicio**, que encapsula varios servicios de IA en uno solo.
  **✔️ Recursos independientes:** Te permiten crear solo los servicios específicos que necesitas. Cada uno tendrá sus propias claves y endpoint, y puedes elegir regiones distintas por servicio. Además, suelen ofrecer una **SKU gratuita** (nivel Free) para experimentar sin costo.
  **✔️ Recurso multiservicio:** Simplifica la gestión al tener un **solo punto de acceso** y facturación unificada para varios servicios (Lenguaje, Visión, Voz, etc. juntos). Puede ser conveniente si tu solución usa varias capacidades de IA a la vez. *💡 Sugerencia: Al crear un recurso en Azure Portal, verás tanto opciones de servicio individual (ej. “Azure AI Language”) como la opción general “Azure AI Services” (multiservicio). Asegúrate de seleccionar el tipo correcto según lo que necesites; sus íconos y nombres los distinguen.*
* **Disponibilidad regional:** No todos los servicios o modelos de Azure AI están disponibles en todas las regiones de Azure. Es esencial **verificar la región** donde planeas desplegar: asegúrate de que soporte el servicio requerido y de que tu suscripción tenga cuota disponible allí. *Por ejemplo, algunos modelos de Azure OpenAI solo están en regiones específicas.*
  Además, elegir una región cercana a tus usuarios puede reducir la latencia.
* **Costos y facturación:** Los servicios de Azure AI **se facturan según uso** (número de transacciones, caracteres procesados, horas de cómputo, etc., dependiendo del servicio). Antes de comprometerte:

  * Revisa la **documentación de precios** del servicio para entender cómo se cobra (por ejemplo, costo por 1000 llamadas a la API de Análisis de Texto).
  * Utiliza la **Calculadora de Precios de Azure** para estimar el costo mensual según tu volumen esperado de uso y región seleccionada. Podrás ajustar parámetros (cantidad de transacciones, etc.) y obtener un estimado que ayude en la planificación.
* **Aislamiento y combinación:** Puedes optar por crear **solo los recursos necesarios** (grano fino) o usar un **recurso combinado**. Por ejemplo, en desarrollo podrías aprovechar varios servicios dentro de un recurso multiservicio, mientras que en producción prefieras separar cada servicio en su propio recurso para aislar cargas y costos. No hay una única respuesta: depende de la escala y arquitectura deseada.

En todos los casos, una vez creado un recurso de Azure AI, dispondrás de un **endpoint HTTP** exclusivo y dos **claves secretas** para autenticación. Con esto tus aplicaciones cliente pueden invocar las APIs del servicio de forma segura.

**✅ Recomendación:** Para empezar sin costo, crea recursos independientes usando la SKU *Free* (si está disponible). Luego, para consolidar una solución grande, evalúa si migrar a un recurso multiservicio facilita la administración de credenciales y facturación.

**Preguntas de autoevaluación:**

1. ¿Cuál es una **ventaja** de aprovisionar servicios de Azure AI como recursos *independientes* en lugar de un recurso multiservicio?
   a. Administración unificada de varios servicios bajo la misma clave.
   b. Posibilidad de elegir regiones diferentes y aprovechar niveles gratuitos por servicio.
   c. Configuración de red simplificada para todos los servicios a la vez.

2. Al crear un recurso de Azure AI, es importante revisar:
   a. Que el servicio esté disponible en la **región** elegida.
   b. Que exista un nivel gratuito (Free) en ese servicio.
   c. **Ambas** (a) y (b).

3. Para **estimar costos** de usar, por ejemplo, el servicio Azure AI Language con cierto volumen de texto al mes, lo mejor es:
   a. Hacer una suposición manual basada en la experiencia.
   b. Usar la **Calculadora de Precios de Azure** configurando el servicio y volúmenes esperados.
   c. Esperar la primera factura de Azure para ver el costo real.
   
<br><br><br>
## Azure AI Foundry (plataforma de desarrollo de IA)

> 📌 **Concepto clave ➜** **Azure AI Foundry** es una plataforma centralizada en Azure que permite **organizar, administrar y desarrollar proyectos de IA** de forma colaborativa, unificando recursos y herramientas.

Azure AI Foundry es la plataforma **recomendada por Microsoft** para desarrollar soluciones de inteligencia artificial a gran escala en Azure. Si bien puedes trabajar con recursos individuales de Azure AI (creándolos y consumiéndolos directamente), Foundry facilita la **organización centralizada** de recursos, la colaboración en equipo y el control administrativo. Sus características principales incluyen:

* **Interfaz y herramientas integradas:** Foundry ofrece un **portal web visual** específico y también un SDK para interactuar programáticamente. Desde el portal, puedes aprovisionar y gestionar recursos, cargar datos, entrenar modelos y más, todo en un mismo lugar.
* **Estructura jerárquica – Centros y Proyectos:** Foundry organiza el trabajo en dos niveles:

  * **Centros (Hubs):** Son **contenedores de nivel superior** que agrupan recursos de IA compartidos, datos comunes, conexiones y configuraciones de seguridad. Un centro representa un entorno de IA unificado (por ejemplo, a nivel de empresa o departamento) donde se administran de forma centralizada los servicios de Azure AI.
  * **Proyectos:** Son espacios de trabajo **dentro de un Centro** dedicados a soluciones o iniciativas específicas de IA. Cada proyecto suele corresponder a un caso de uso o aplicación (ej: “Chatbot de atención al cliente” o “Clasificación de documentos”). Los proyectos heredan los recursos y configuraciones compartidas del centro padre, y permiten a los equipos colaborar enfocándose en su solución concreta.

**➕ Al crear un nuevo Centro** en Azure AI Foundry (a través del portal), se aprovisionan automáticamente varios recursos base en tu suscripción Azure, necesarios para habilitar la plataforma:

* Un **recurso de Azure AI multiservicio** (Services Hub) que incluye acceso a varios servicios de Azure AI (por ejemplo, incluye Azure OpenAI, Language, Vision, etc. bajo el mismo recurso).
* Un **Azure Key Vault** para almacenar de forma segura secretos y claves (por ejemplo, credenciales, strings de conexión) necesarios en proyectos.
* Una **cuenta de Azure Storage** para alojar datos del centro y de los proyectos (archivos, datos de entrenamiento, outputs, etc.).
* *Opcional:* un **recurso Azure AI Search** dedicado, útil para indexar datos dentro del centro y habilitar técnicas de *grounding* en soluciones de IA generativa (por ejemplo, para buscar contexto relevante para un modelo GPT).

*(Es obligatorio contar con al menos un Centro para aprovechar todas las funcionalidades de Foundry. Puedes crear varios Centros si deseas aislar recursos entre diferentes unidades organizativas.)*

Una vez creado el Centro, los equipos pueden crear **Proyectos** dentro de él según necesiten. Todos los **recursos compartidos** definidos en el Centro (p. ej. servicios Azure AI o bases de datos conectadas) estarán **disponibles en cada proyecto** automáticamente, sin que los desarrolladores de cada proyecto deban configurarlos uno por uno. Esto ahorra tiempo y evita problemas de permisos.

* **Colaboración y control de acceso unificado:** Azure AI Foundry centraliza la administración de usuarios y permisos mediante **roles** predefinidos a nivel de Centro y a nivel de Proyecto:

  * *Roles a nivel Centro:* por ejemplo, **Propietario del centro** (control total, incluido gestionar permisos y crear nuevos centros), **Colaborador** (control total salvo administrar permisos), **Azure AI Developer** (puede usar y administrar recursos, sin gestionar permisos ni centros), **Operador de implementación de IA** (puede desplegar modelos en infraestructuras de inferencia), y **Lector** (solo lectura). El creador del Centro es Propietario por defecto.
  * *Roles a nivel Proyecto:* **Propietario del proyecto** (control total del proyecto, incluidas sus configuraciones y permisos), **Colaborador** (puede modificar todo en el proyecto menos permisos), **Azure AI Developer (Proyecto)** (puede realizar tareas de desarrollo/implantación en el proyecto, sin tocar permisos), **Operador de inferencia** (despliega recursos/modelos en runtime), **Lector** (consulta datos pero no modifica nada).
    *Nota:* Los miembros asignados a un proyecto reciben automáticamente permisos de Lector en el Centro asociado, para poder acceder a los recursos compartidos. Un administrador de TI suele ser quien asigna quién es miembro de qué proyectos y con qué rol, manteniendo la seguridad centralizada.
* **Recursos conectados:** Foundry permite **conectar recursos de Azure externos** ya existentes (o nuevos) tanto a nivel de Centro como de Proyecto:

  * Recursos conectados al **Centro** quedan disponibles automáticamente en **todos sus proyectos** (a través de un mecanismo de proxy, de forma que los usuarios del proyecto pueden usarlos sin tener credenciales directas). Esto es ideal para fuentes de datos o servicios compartidos por todos.
  * Si un proyecto necesita algún recurso específico *no compartido* con otros proyectos, se puede conectar únicamente a ese proyecto. Por ejemplo, si solo el Proyecto A requiere una base de datos X, se conecta allí y no en el Centro.
  * **✅ Recomendación:** Planifica estratégicamente qué recursos deberían conectarse al nivel Centro (para heredarlos globalmente) y cuáles a nivel de proyecto, según si serán usados de forma común o aislada. Esto facilita la administración y minimiza solicitudes de acceso innecesarias.
* **Herramientas integradas en proyectos:** Dentro de cada proyecto en Foundry, los desarrolladores tienen acceso a herramientas que agilizan el ciclo de desarrollo de IA:

  * **Catálogo de modelos:** para explorar y desplegar fácilmente modelos de IA, ya sea de Azure OpenAI (modelos GPT, etc.) o de una biblioteca como Hugging Face.
  * **Playgrounds (entornos de prueba):** áreas interactivas para probar *prompts* y configuraciones con modelos generativos en tiempo real, afinando la interacción antes de codificarla.
  * **Acceso rápido a servicios Azure AI:** interfaz visual para probar llamadas a los servicios (por ejemplo, analizar una imagen con Vision) y obtener **códigos de ejemplo** (snippet) en C#, Java o Python listos para usar en tu app.
  * **Entornos de desarrollo con VS Code:** posibilidad de crear **instancias de Visual Studio Code en contenedor** directamente desde Foundry, que corren en la nube pero accesibles vía navegador o remotamente. Estos entornos vienen pre-configurados con los últimos SDK de Azure AI, evitando instalar nada localmente. *(⚠️ Importante: Ten en cuenta que usar un VM/contendor para VS Code en la nube consume recursos de cómputo Azure; planifica bien su uso para no exceder cuotas ni incurrir en costos inesperados.)*
  * **Fine-tuning (ajuste fino):** herramientas para personalizar modelos de IA generativa (como GPT) con datos específicos, de modo que sus respuestas se adapten mejor al contexto deseado.
  * **Prompt Flow:** un orquestador visual para flujos conversacionales complejos, permitiendo encadenar llamadas a modelos generativos con lógica (condiciones, bucles), integrando también pasos de filtrado o postprocesamiento.
  * **Monitoreo y seguridad integrados:** paneles para hacer seguimiento al rendimiento de modelos y detectar sesgos o problemas, e integración con **Seguridad de Contenido** para moderar la salida de modelos generativos (ej: filtrar respuestas antes de entregarlas al usuario final).
  * **Gestión de activos del proyecto:** sección centralizada donde ver todos los **elementos del proyecto**: modelos desplegados, endpoints disponibles, conjuntos de datos almacenados, índices creados con Azure Search e incluso aplicaciones web o APIs que hayas implementado dentro del proyecto.

Con Azure AI Foundry, en resumen, se busca **centralizar la administración** (recursos, costos, seguridad) al mismo tiempo que se **agiliza el trabajo colaborativo** en IA. En vez de que cada equipo maneje por separado sus servicios de IA, Foundry provee un **hub unificado** donde todo está organizado por proyectos pero gobernado desde el centro.

**🔒 Seguridad y gobierno:** Foundry sigue buenas prácticas de seguridad corporativa. Un administrador de TI puede gestionar todos los accesos desde el nivel Centro, asegurando cumplimiento de políticas. Los registros de actividad quedan centralizados, facilitando auditorías. Además, se puede integrar con Azure AD para usar grupos de seguridad existentes.

**💡 Nota:** No todos los servicios o características de Azure AI Foundry están disponibles globalmente. Algunas funciones pueden variar según la región de Azure donde se habilite Foundry. Siempre verifica la **disponibilidad regional de Foundry** para tu ubicación y, de ser necesario, solicita acceso previo si alguna característica está en vista previa limitada.

**💰 Costos en Foundry:** Además del costo normal por uso de los servicios de IA subyacentes, Foundry agrega costos de los **recursos de apoyo** (almacenamiento, instancias de contenedores VS Code, etc.). También existen **cuotas (limits)** a nivel de Foundry, por ejemplo en cantidad de proyectos, llamadas por minuto, etc., para proteger los recursos. Si necesitas mayor capacidad (por ejemplo, más throughput de OpenAI), puedes gestionar aumentos de cuota con Azure. Planifica estos aspectos en tu presupuesto de proyecto.

**Preguntas de autoevaluación:**

1. Dentro de Azure AI Foundry, ¿qué diferencia principal existe entre un **Centro** y un **Proyecto**?
   a. Un *Centro* agrupa recursos y configuraciones compartidas, mientras un *Proyecto* es un espacio de trabajo específico que hereda esos recursos para una solución particular.
   b. Un *Proyecto* contiene varios Centros en su interior para organizar recursos.
   c. No hay diferencia, son términos sinónimos en Foundry.

2. Al **crear un Centro** en Azure AI Foundry, ¿cuál de los siguientes recursos se **aprovisiona automáticamente**?
   a. Un Key Vault para secretos del Centro.
   b. Un clúster de Kubernetes para despliegues.
   c. Un servidor on-premises dedicado.

3. ¿Cuál de estos es un **beneficio clave** de usar Azure AI Foundry en vez de trabajar con servicios de Azure AI individuales por separado?
   a. Permite gestionar centralmente accesos, costos y recursos compartidos entre proyectos.
   b. Evita completamente todos los costos asociados a los servicios de Azure AI.
   c. Elimina la necesidad de entrenar modelos o escribir código en proyectos de IA.
   
<br><br><br>
## Inteligencia artificial **responsable**

> 📌 **Concepto clave ➜** **IA Responsable** se refiere a un conjunto de **principios éticos y buenas prácticas** (imparcialidad, transparencia, privacidad, etc.) que buscan asegurar que los sistemas de IA sean **justos, confiables y seguros** para la sociedad.

Al desarrollar e implementar soluciones de IA, es fundamental considerar el impacto social y ético. Microsoft promueve **6 principios de IA Responsable** que deben guiar cualquier proyecto de IA para mitigar riesgos:

* ⚖️ **Imparcialidad:** La IA debe **tratar a todas las personas de manera justa**, evitando sesgos o discriminación por género, etnia, edad, etc. Esto implica escoger datos de entrenamiento **representativos** y evaluar el desempeño del modelo en distintos subgrupos. *Por ejemplo:* verificar que un modelo de reconocimiento facial funcione igual de bien con diferentes tonos de piel. Si se detectan sesgos, se deben ajustar datos o algoritmos. **💡 Nota:** Existen herramientas técnicas para detectar y reducir sesgos, pero ninguna sustituye la **supervisión humana** continua.
* 🛡️ **Confiabilidad y seguridad:** Los sistemas de IA deben ser **seguros y predecibles**. En aplicaciones críticas (vehículos autónomos, diagnóstico médico, etc.) se exige un comportamiento altamente confiable. Esto requiere **pruebas rigurosas** antes de desplegar, monitoreo en producción, y tener en cuenta que los modelos dan **respuestas probabilísticas** (no absolutas). Es importante establecer **umbrales de confianza** y manejar de forma segura errores o incertidumbres. La IA no debe hacer nada fuera del alcance esperado y siempre debería haber mecanismos de respaldo si falla.
* 🔒 **Privacidad y seguridad (de datos):** Se debe **proteger la información personal y sensible** en todo el ciclo de vida de la IA. Esto significa cumplir regulaciones de privacidad (GDPR, etc.), anonimizar o encriptar datos personales, y limitar el acceso a los datos y resultados solo a quienes corresponda. Implementa controles de seguridad robustos para evitar brechas de datos. *Ejemplo:* si entrenas un modelo con historiales médicos, asegúrate de remover identificadores personales y de resguardar los datos en entornos seguros.
* 🌐 **Inclusión:** La IA debe ser **accesible y beneficiosa para todas las personas**, independientemente de sus capacidades, idioma, cultura o antecedentes. Esto implica diseñar con **diversidad** en mente: incluir en el equipo de desarrollo a personas con distintas perspectivas, y probar la IA con diversos usuarios (incluyendo personas con discapacidades) para garantizar que nadie quede excluido. *Ejemplo:* un asistente de voz debería entender acentos distintos y manejar bien voces femeninas y masculinas por igual.
* 🔎 **Transparencia:** Los sistemas de IA deben ser **comprensibles** y comunicativos sobre su funcionamiento. A los usuarios se les debe informar cuando están interactuando con una IA (y no con un humano), qué datos utiliza el sistema, cómo llegó a ciertas decisiones (en la medida de lo posible) y con qué nivel de confianza. La **explicabilidad** es clave: aunque modelos complejos como redes neuronales sean cajas negras, se deben proporcionar explicaciones o justificaciones apropiadas para generar confianza. *Ejemplo:* en un sistema de reconocimiento facial en público, informar claramente su presencia y propósito, y permitir a las personas saber si fueron reconocidas.
* 🏅 **Responsabilidad:** Las personas y organizaciones deben **asumir responsabilidad por los resultados** de sus sistemas de IA. Esto significa que los desarrolladores y propietarios de la IA son responsables de su **comportamiento**, de la **calidad de los datos** con que fue entrenada y de las **acciones** que derive. Debe haber **supervisión humana** y mecanismos de rendición de cuentas. Cualquier sistema de IA debe operar dentro de un marco de **gobernanza** con estándares legales y éticos bien definidos. En caso de error o daño, una persona o entidad debe poder responder y corregirlo.

Aplicando estos principios, buscamos minimizar riesgos como discriminación algorítmica, decisiones incorrectas que afecten negativamente a personas, invasión de la privacidad o falta de transparencia que genere desconfianza. En la práctica, incorporar IA responsable podría implicar acciones como: auditorías de sesgo en los modelos, evaluaciones de impacto ético antes del despliegue, documentación clara del propósito y limitaciones de la IA, y capacitación a los equipos en ética de datos.

**✅ Resumen de IA Responsable:**
Desarrolla tus soluciones de IA de forma que sean **justas (fairness)** con todos los usuarios, **seguras y confiables (reliable & safe)** en su funcionamiento, **privadas (private)** con los datos de las personas, **inclusivas (inclusive)** para toda la comunidad, **transparentes (transparent)** en su lógica y resultados, y siempre con **responsabilidad (accountability)** humana detrás para supervisar y responder por la IA.

**Preguntas de autoevaluación:**

1. Un modelo de IA clasifica sistemáticamente peor las solicitudes de cierto grupo demográfico. ¿Qué principio de IA responsable se está violando principalmente?
   a. Imparcialidad
   b. Transparencia
   c. Inclusión

2. Informar al usuario sobre las limitaciones y margen de error de un sistema de IA, así como explicar cómo llegó a cierta decisión, ayuda a cumplir el principio de:
   a. Privacidad
   b. Transparencia
   c. Confiabilidad

3. **Verdadero o Falso:** Un desarrollador no necesita preocuparse por sesgos en los datos de entrenamiento si su modelo de IA tiene alta precisión global.
   
<br><br><br>
## Creación y consumo de los servicios de Azure AI

> 📌 **Concepto clave ➜** Los servicios de Azure AI son **API en la nube**. Para usarlos debes aprovisionar un recurso (obtener endpoint + claves) y luego consumirlo ya sea mediante **llamadas REST** o con **SDKs** oficiales.

Los Servicios de Azure AI son **componentes modulares**: se crean como recursos en Azure y luego se **consumen desde tus aplicaciones**. Veamos el ciclo básico:

1. **Aprovisionar un recurso:** En el portal de Azure (o por CLI/plantillas) creas, por ejemplo, un recurso de *Azure AI Language*. Al hacerlo, defines la región y obtienes las **claves de suscripción** y la **URL endpoint** para ese servicio.
2. **Configurar acceso:** Anota el **URI del endpoint** (p. ej. `https://turecurso.cognitiveservices.azure.com/`) y las **claves** (Azure siempre genera dos claves por recurso para facilitar la rotación). También recuerda la **región** asociada (p. ej. *westeurope*); algunos SDK te la pedirán.
3. **Consumir la API:** Tienes dos opciones principales:

   * Invocar la API REST directamente mediante **HTTP** (enviando datos JSON en las solicitudes y recibiendo JSON en las respuestas).
   * Usar un **SDK (kit de desarrollo)** específico del lenguaje, que internamente llama a la API REST pero te expone funciones/metodos más amigables.

### Aprovisionamiento: tipos de recurso y claves

Al crear recursos de ciertos servicios, Azure puede pedir más detalles:

* Algunos servicios distinguen entre **recursos de “entrenamiento” y de “predicción”**. Por ejemplo, en la antigua versión de LUIS (Language Understanding) se usaban separadamente un recurso para entrenar modelos personalizados y otro para ejecutarlos (inferir) una vez entrenados. La razón es que el entrenamiento consume mucho cómputo (y se cobra distinto) mientras que la predicción es más ligera pero frecuente. **Ejemplo:** Azure AI Custom Vision aún separa *Training* y *Prediction* endpoints: entrenas tu modelo de visión en un recurso, y despliegas el modelo a un endpoint de predicción para consultarlo.
* En general, al aprovisionar cualquier recurso de Azure AI, se generan los siguientes elementos clave para poder usarlo:

  * **URI del endpoint:** Dirección base para las API. Ej: `https://<nombre-recurso>.api.cognitive.microsoft.com/` o con formato regional `https://<nombre>.cognitiveservices.azure.com/`. Todas las solicitudes REST se construyen a partir de esta URL.
  * **Claves de suscripción:** Se proporcionan **2 claves** (iguales en permisos) por recurso. Estas claves son secretas y se envían en las llamadas para autenticarte. Tener dos permite rotarlas (cambiarlas periódicamente) sin interrumpir el servicio.
  * **Ubicación/Región:** La región Azure donde reside el recurso (p. ej. *eastus*, *japaneast*, etc.). Algunos SDK necesitan que especifiques esta región al inicializar el cliente, para saber a dónde conectarse. Si usas la API REST directamente, generalmente la URL del endpoint ya incluye la región.

Una vez tienes un recurso con su endpoint y key, **puedes consumir el servicio** desde cualquier entorno: página web, aplicación móvil, backend, etc., simplemente realizando llamadas HTTP autenticadas.

### Uso de API REST

Los servicios Azure AI exponen endpoints **RESTful**. Esto significa que cada funcionalidad (por ejemplo, detectar el idioma de un texto, analizar sentimiento, reconocer caras en una imagen, etc.) se logra haciendo una **petición HTTP** a la URL correspondiente con los datos adecuados. Características del uso vía REST:

* Se suele usar el método HTTP apropiado (GET, POST, etc.) según la operación, aunque la mayoría de las operaciones de análisis usan **POST** (envías datos en el cuerpo).
* La **autenticación** se realiza enviando en los headers de la petición tu **clave de suscripción** (por ejemplo, usando el header `Ocp-Apim-Subscription-Key: <tu_clave>`). Si tu recurso es *multiservicio*, a veces debes enviar también un header de región, e.j. `Ocp-Apim-Subscription-Region: <tu_región>`.
* El contenido (request y response) es en **formato JSON**. Tú envías los parámetros o datos de entrada en JSON (por ejemplo, una lista de textos a analizar) y el servicio devuelve un JSON con los resultados (ej. idiomas detectados con sus puntuaciones).
* **Independencia de lenguaje:** cualquier lenguaje de programación o herramienta capaz de hacer solicitudes HTTP y manejar JSON puede usar estas APIs. Esto incluye lenguajes como Python, C#, Java, JavaScript, PHP, Go, Ruby, etc., y también herramientas como **Postman** o simplemente `curl` en la terminal.

*Ejemplo (REST):* Supongamos que quieres traducir un texto al español usando Azure Translator. Podrías hacer una solicitud REST así:

```bash
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&to=es" \
  -H "Ocp-Apim-Subscription-Key: <TU_CLAVE>" \
  -H "Ocp-Apim-Subscription-Region: <TU_RECURSO_REGION>" \
  -H "Content-Type: application/json" \
  -d "[{ 'Text': 'Hello, world!' }]"
```

Esta llamada HTTP envía un JSON con el texto `"Hello, world!"` y en la URL solicita la traducción a español (`to=es`). El servicio responderá con un JSON que incluye `"Hola, mundo!"` como traducción, entre otros datos (lengua detectada, puntuación de confianza, etc.).

Como se ve, usar REST **no requiere librerías especiales**, solo la URL correcta, los headers de autenticación y el formato JSON adecuado. Es ideal para pruebas rápidas o integraciones en entornos donde no hay un SDK disponible.

### Uso de un SDK

Aunque las APIs REST son abiertas, Azure proporciona **SDKs oficiales** para muchos lenguajes (C#, Python, JavaScript/TypeScript, Java, Go, etc.). Un SDK es una biblioteca que **simplifica el trabajo** al envolver esas llamadas REST en funciones/clases de más alto nivel. Ventajas de usar SDK:

* **Menos código y errores:** en lugar de armar manualmente solicitudes HTTP, llamas métodos con parámetros nativos. El SDK construye la petición, la envía y parsea la respuesta por ti.
* **Manejo de autenticación integrado:** típicamente solo pasas la clave (o credenciales) al inicializar el cliente del SDK, y luego todas las llamadas se autentican automáticamente.
* **Modelos de objetos:** las respuestas se reciben ya convertidas a objetos o estructuras propias del lenguaje, facilitando su manejo (en vez de navegar un JSON bruto).
* **Actualizaciones y mejores prácticas:** los SDK suelen implementar buenas prácticas (reintentos, paginación, gestión de tokens, etc.) y se actualizan con nuevas funcionalidades.

**Ejemplo (SDK en Python):** A continuación, un snippet usando el SDK de Azure AI Text Analytics (Lenguaje) en Python, para analizar el **sentimiento** de un texto:

```python
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential

endpoint = "https://<mi-recurso>.cognitiveservices.azure.com/"
clave = "<mi_clave_de_acceso>"

# Autenticación del cliente con endpoint y credencial
cliente = TextAnalyticsClient(endpoint=endpoint, credential=AzureKeyCredential(clave))

# Datos de entrada: lista de textos a analizar
documentos = ["El servicio Azure AI es genial"]

# Llamada al servicio de análisis de sentimiento
respuesta = cliente.analyze_sentiment(documentos)

# Procesar la respuesta
for doc in respuesta:
    print(doc.sentiment, doc.confidence_scores)
    # Ej output: "positive SentimentConfidenceScores(positive=1.0, neutral=0.0, negative=0.0)"
```

En este código, el SDK maneja internamente la comunicación REST. Solo proporcionamos el endpoint y la clave una vez, y luego llamamos `analyze_sentiment`. Obtenemos directamente un objeto `doc` con propiedades: `doc.sentiment` podría ser `"positive"` (positivo) y `doc.confidence_scores` trae las puntuaciones de confianza para positivo/neutral/negativo.

**SDK disponibles:** Los nombres varían pero generalmente hay un paquete por servicio. Por ejemplo, en .NET existe `Azure.AI.TextAnalytics`, `Azure.AI.Vision`, etc.; en Python `azure-ai-formrecognizer`, `azure-ai-translation-text`, etc. Cada SDK viene con **documentación detallada** de clases y métodos, y a menudo con **ejemplos** en la documentación de Microsoft Learn.

En resumen, usar REST te da flexibilidad (útil para *quick hacks* o lenguajes sin SDK), mientras que usar un SDK te acelera el desarrollo y reduce errores, sobre todo en proyectos grandes. Puedes empezar probando las APIs con herramientas REST y luego pasar a un SDK en tu lenguaje preferido para la implementación final.

**Preguntas de autoevaluación:**

1. ¿Qué formato de datos se utiliza para enviar y recibir información al usar las APIs REST de Azure AI?
   a. XML
   b. JSON
   c. YAML

2. Una **ventaja** de usar el SDK oficial en lugar de llamar a la API REST directamente es:
   a. No necesitas preocuparte por manejar las autenticaciones o peticiones HTTP manualmente, el SDK simplifica esas tareas.
   b. El SDK permite usar las funciones sin necesidad de un endpoint o clave.
   c. Los SDK son la única forma de llamar a los servicios Azure AI (no se puede vía REST).

3. **Verdadero o Falso:** Cualquier lenguaje de programación capaz de realizar solicitudes HTTP puede utilizar los servicios de Azure AI mediante las APIs REST.
   
<br><br><br>
## Autenticación y gestión de acceso a los servicios

> 📌 **Concepto clave ➜** La **autenticación** de Azure AI garantiza que solo usuarios o apps autorizadas accedan al servicio. Se logra mediante **claves secretas** de suscripción o integrando con **Azure AD (Microsoft Entra ID)** para usar identidades seguras.

La seguridad es primordial: tus servicios de Azure AI pueden procesar datos sensibles, por lo que debes proteger su acceso. Azure proporciona varias **capas de autenticación y control de acceso**:

* **Claves de suscripción (APIs):** Por defecto, cada recurso de Azure AI se protege con las **claves** mencionadas. Solo quienes tengan una clave válida podrán invocar la API. Es fundamental **mantener estas claves secretas** (no exponerlas públicamente en código front-end, repositorios, etc.). Si sospechas que una clave se filtró, **regenerar la clave** inmediatamente (las UI de Azure permiten invalidar una clave y generar una nueva).
* **Rotación de claves:** Azure te da *dos* claves activas para cada recurso precisamente para que puedas rotarlas sin downtime. Un proceso recomendado de **rotación** periódica sería:

  1. Configura todas tus aplicaciones clientes para que usen **solo la “Clave 1”** inicialmente.
  2. Cuando quieras rotar, en Azure Portal pulsa *Regenerar* sobre la **Clave 2**. Obtendrás una nueva clave2 secreta.
  3. Actualiza tus aplicaciones para que ahora utilicen esta **Nueva Clave 2** en lugar de la 1.
  4. Luego ve al portal y *Regenera* la **Clave 1**.
  5. Finalmente, cambia las apps para que vuelvan a usar la **Nueva Clave 1**. (Quedará la clave2 como backup para la siguiente rotación).
     De este modo, nunca te quedas sin una clave válida durante el proceso. *🔐 Consejo:* Realiza rotaciones de clave de forma regular (ej. cada 90 días) para limitar el tiempo de exposición en caso de filtración.
* **Almacenamiento seguro de claves:** No embebas claves en código fuente ni config files sin cifrar. En su lugar, utiliza servicios como **Azure Key Vault**: un almacén centralizado de secretos seguro. Puedes guardar allí las claves de tus recursos Azure AI y tu aplicación las solicita al Vault de forma segura en tiempo de ejecución. **Azure Key Vault** se integra con la identidad de Azure AD de tu aplicación, evitando que necesites exponer la clave en ningún momento. *(Es decir, tu app obtiene un token de Azure AD, con él lee la clave del Key Vault, y luego llama al servicio AI.)*
* **Tokens de acceso (Auth tokens):** Algunos servicios (por ejemplo, Azure Cognitive Search o ciertos endpoints de vision) permiten intercambiar la clave por un **token JWT temporal** (válido \~10 minutos) que se usa para invocar la API. Este mecanismo añade seguridad al no enviar la clave en cada llamada, sino un token efímero. Los SDK normalmente se encargan de gestionar estos tokens tras bastidores si aplica, por lo que como desarrollador casi no lo notas.
* **Autenticación con Azure AD (Microsoft Entra ID):** Es la alternativa **más segura y recomendada** especialmente en entornos empresariales. Consiste en **no usar claves estáticas**, sino dar acceso al servicio a identidades Azure AD (aplicaciones o usuarios) mediante **Roles**. Dos enfoques comunes:

  * **Entidades de servicio (Service Principal):** Registras una **aplicación en Azure AD** que represente a tu aplicación cliente. Luego configuras tu recurso Azure AI para que confíe en esa identidad. En la práctica:

    1. **Habilitar un subdominio personalizado** en tu recurso de Cognitive Services (esto convierte tu recurso para aceptar Azure AD). Ejemplo de subdominio: `midominio.cognitiveservices.azure.com`. *(Esto se hace una sola vez al crear el recurso, con PowerShell o CLI.)*
    2. **Registrar una app** en Azure AD (desde el portal Azure AD -> Registros de aplicaciones). Obtendrás un *Client ID* y puedes generar un *secreto* o certificado para esa app.
    3. **Crear la entidad de servicio** para esa app (Azure AD te permite convertir esa app en una identidad utilizable para auth de recursos Azure).
    4. **Asignar rol en el recurso:** Ir al recurso Azure AI -> pestaña "Control de acceso (IAM)" -> Agregar rol *Cognitive Services User* (o *Cognitive Services Contributor* según nivel de acceso deseado) a la entidad de servicio creada.
       Una vez hecho esto, tu aplicación puede obtener un **token OAuth2** desde Azure AD usando su ClientID/secret, y usar ese token (Bearer) para autenticar llamadas al servicio en lugar de la clave. Esto permite revocar permisos centralmente, usar autenticación basada en certificados, etc.
  * **Identidades administradas:** Azure ofrece *Managed Identity* para servicios como máquinas virtuales, Azure Functions, etc. Una **identidad administrada** es una identidad de Azure AD que Azure **gestiona por ti** (rotación automática de credenciales). Puede ser *Asignada por el sistema* (ligada a un recurso Azure específico, p.ej. a una VM; se crea y borra con ella) o *Asignada por el usuario* (una identidad independiente que puedes asociar a varios recursos).
    **Uso típico:** habilitas una identidad administrada en tu aplicación (por ejemplo, en la VM donde corre tu código). Luego vas a tu recurso Azure AI y en IAM le das rol de **Colaborador/Usuario de Cognitive Services** a esa identidad. Así, cuando tu código en la VM llame al servicio Azure AI, no necesita clave: la VM puede obtener un token de Azure AD automáticamente representando su identidad y la llamada será autenticada. *(Esto mejora la seguridad porque no hay claves a manejar manualmente.)*
    *Ejemplo:*

    * Habilitas identidad administrada en tu VM con `az vm identity assign ...`. Azure le asignará un Object ID en AD.
    * En el recurso Azure AI: IAM -> Agregar asignación -> Rol “Cognitive Services User” -> Asignar a **Identidad administrada** -> Seleccionas tu VM como entidad -> Asignar.
      Ahora la VM (y el código que corre en ella) tiene permisos para usar ese recurso AI. En código, dentro de la VM, podrías usar por ejemplo el SDK de Azure con `DefaultAzureCredential` (que detecta la Managed Identity automáticamente) en lugar de AzureKeyCredential.

    **Nota:** Para que la autenticación Azure AD funcione en tu recurso de Azure AI, este debe tener un subdominio personalizado configurado (si se creó recientemente vía Foundry probablemente ya lo tenga). Revisa la documentación si es un recurso antiguo.

En resumen, **iniciar con claves** es sencillo, pero a medida que la solución crece conviene pasar a **Azure AD** por un control más granular:

* En entornos de desarrollo pequeños quizá uses la clave en variables de entorno.
* En producción, **lo ideal** es que ninguna clave esté expuesta: uses identidades administradas o entidades de servicio con roles. Así puedes revocar accesos rápidamente y seguir el principio de privilegio mínimo.

**⚠️ Importante:** Siempre que alguien deja de necesitar acceso (p.ej. un empleado que sale del proyecto), quítalo de los roles en Foundry/recursos Azure AD. Y si usaban claves compartidas, considera regenerarlas.

**Preguntas de autoevaluación:**

1. De forma predeterminada, ¿cómo se restringe el acceso a un recurso de Azure AI recién creado?
   a. Mediante un nombre de usuario y contraseña.
   b. Mediante **claves de suscripción** que deben incluirse en cada llamada.
   c. No tiene ninguna restricción, es público por defecto.

2. ¿Cuál es una ventaja de usar una **Identidad Administrada de Azure** en lugar de una clave de suscripción para que una aplicación acceda a un servicio de Azure AI?
   a. La identidad administrada se rota automáticamente y no requiere almacenar claves manualmente, aumentando la seguridad.
   b. Es la única forma de acceder a servicios Azure AI, las claves dejarán de funcionar.
   c. Evita tener que crear una aplicación en Azure AD o roles.

3. **Completa la frase:** Azure Key Vault se utiliza principalmente para...
   a. almacenar y proteger claves y secretos de aplicaciones, como las claves de Azure AI, de forma segura.
   b. aumentar la velocidad de las consultas a servicios cognitivos.
   c. reemplazar la necesidad de Azure AD en la autenticación.
   
<br><br><br>
## Seguridad de red para los servicios de Azure AI

> 📌 **Concepto clave ➜** La **seguridad de red** permite limitar qué orígenes pueden conectarse a tu servicio Azure AI, usando firewalls, redes virtuales y puntos de conexión privados, para evitar accesos no autorizados desde Internet.

Por defecto, cuando creas un recurso de Azure AI (por ejemplo un servicio de Lenguaje), este está **accesible desde cualquier red en Internet** siempre que se tenga la clave correcta. Aunque la clave brinda seguridad, en entornos empresariales es recomendable añadir una capa adicional restringiendo el acceso de red. Azure soporta varias configuraciones:

* **Acceso de red predeterminado: Todas las redes (público)** – *Valor por defecto.* Significa que **no hay restricciones de red**: cualquier cliente desde Internet puede intentar conectarse al endpoint (si no tiene la clave, igual no podrá usarlo, pero el recurso es alcanzable públicamente).
* **Redes seleccionadas y Endpoints privados:** En esta configuración, **solo** las direcciones IP o las redes virtuales de Azure explícitamente permitidas podrán acceder al recurso. Es el modo ideal para aislar tu servicio. Puedes, por ejemplo, permitir solo la red de tu aplicación en Azure (VNet) y la IP fija de tu oficina. Todo lo demás sería bloqueado a nivel de red, incluso si alguien conoce la clave. También permite el uso de **Private Endpoints** (ver más abajo).
* **Acceso deshabilitado (solo endpoint privado):** Con esta opción marcada, el servicio **bloquea todo tráfico entrante** que no provenga de un **Punto de conexión privado**. Es la modalidad más estricta: obliga a consumir el servicio únicamente a través de la red interna de Azure (o redes conectadas via VPN/ExpressRoute) mediante un endpoint privado asociado. En otras palabras, el servicio queda **completamente aislado de Internet público**.

Para configurar estas opciones, se realiza desde el Azure Portal, en la sección **"Redes"** del recurso Azure AI:

1. Navega al recurso (p.ej. tu recurso *Cognitive Services*).
2. En el menú lateral, bajo "Configuración", elige **Redes**. Allí verás la opción de seleccionar el nivel de acceso.
3. Si eliges *"Redes seleccionadas y puntos de conexión privados"*, aparecerán secciones para agregar **redes virtuales** y **reglas de firewall (IPs)**:

   * Para **permitir una red virtual de Azure:** haz clic en *Agregar red virtual*. Selecciona la suscripción, la VNet y la subred específicas desde las que permitir el acceso. (Nota: la VNet debe tener habilitado el *Servicio de extremo* de `Microsoft.CognitiveServices` para conectar con servicios cognitivos; Azure Portal suele guiarte para activarlo si no lo está, esto puede tardar \~15 min).
   * Para **permitir IPs específicas (firewall):** en la sección de firewall agrega las direcciones IP públicas (o rangos CIDR) que deban tener acceso. Por ejemplo, la IP pública de tu servidor on-premises o tu rango corporativo de salida a internet.
   * Guarda los cambios. En unos minutos las reglas quedarán activas.
4. *Opcional:* Si vas a usar **Private Endpoints**, igual debes tener la opción de *Redes seleccionadas* activa (o la de *Deshabilitado* en última instancia), porque un endpoint privado cuenta como red autorizada especial.

**⚠️ Importante:** Si cambias el acceso predeterminado a *deny all* (Deshabilitado) **antes** de configurar redes o endpoints permitidos, **bloquearás todo acceso** (incluso el tuyo). Por eso, **primero** agrega las excepciones necesarias (VNet, IPs o endpoints privados) y luego, cuando confirmes que funcionan, puedes optar por bloquear totalmente el resto.

### Puntos de conexión privados (Private Endpoints)

Un **Private Endpoint** te permite asignar una **dirección IP privada** dentro de tu red virtual de Azure que apunte a tu servicio de Azure AI. En efecto, tu servicio se “asoma” dentro de tu red como si fuera un recurso más de ella, evitando la ruta por internet pública. Cualquier tráfico hacia esa IP privada viaja por la red interna de Azure.

**Pasos simplificados para crear un Private Endpoint:**

1. En la misma página de **Redes** del recurso Azure AI, busca la sección **Conexiones de punto de conexión privado** y haz clic en *+ Punto de conexión privado*. Se abre un asistente.
2. Elige la suscripción y grupo de recursos donde crear el endpoint (generalmente el mismo de tu VNet). Asigna un nombre al endpoint privado y a la interfaz de red que se generará.
3. En la pestaña **Recurso**, verifica que va a conectar al recurso correcto (debería detectar automáticamente tu servicio de Azure AI actual como destino).
4. En la pestaña **Red virtual**, selecciona la **VNet y subred** donde quieres que viva la IP privada que representará al servicio. (Debe ser una subred que tenga visibilidad desde tu aplicación cliente).
5. Deja habilitada la integración DNS privada si sale la opción, para que Azure gestione los registros DNS necesarios (esto permitirá que cuando en tu red alguien busque el host `<tu-recurso>.cognitiveservices.azure.com`, resuelva a la IP privada).
6. Finaliza la creación. Azure aprovisionará el endpoint privado y lo asociará con tu servicio (esto suele crear también un NIC en la subred elegida). Una vez completado, tu servicio tendrá una conexión privada **Pendiente de aprobación**.
7. Ve nuevamente a la sección de Conexiones de punto de conexión privado, deberías ver la solicitud. Apruébala (Azure a veces la aprueba automáticamente si eres el mismo dueño de ambos recursos). Al aprobar, el estado pasará a Conectado.

Ahora tu recurso Azure AI tiene un endpoint dentro de la VNet. Puedes probar desde una máquina en esa VNet hacer ping o nslookup al nombre del servicio; debería resolver a la IP privada y ser accesible (recuerda enviar la clave en las peticiones aún).

*Uso completo privado:* Una vez operativo el endpoint privado, puedes incluso cambiar la opción de red del recurso a **Deshabilitado** (denegar todo lo público). Así **obligas** a que **todas las conexiones** ocurran vía ese endpoint privado, reforzando la seguridad.

### Servicios de confianza de Azure

Azure define un conjunto de **servicios de confianza** (Trusted Azure Services) que pueden, si tú lo permites, comunicarse con tu recurso de Azure AI incluso si el acceso está restringido. Esto es útil, por ejemplo, si cierras todo acceso público pero quieres que un servicio como Azure Machine Learning (o Azure AI Foundry mismo) pueda seguir llamando a tu recurso internamente.

Algunos **servicios de confianza** relevantes:

* Azure Machine Learning (incluye Azure AI Foundry) – *Proveedor:* `Microsoft.MachineLearningServices`
* Azure AI Search – *Proveedor:* `Microsoft.Search`
* (Generalmente cualquier servicio listado bajo `Microsoft.CognitiveServices` también es intrínsecamente de confianza frente a sí mismo.)

En la sección de **Redes** del recurso, verás una casilla que dice: *“Permitir que los servicios de Azure de la lista de servicios de confianza accedan a esta cuenta de Cognitive Services”*. Si la activas, estos servicios podrán saltarse las reglas de red **pero** siempre **autenticándose** con su identidad administrada. Es decir, Foundry (por ejemplo) usará su Managed Identity para acceder, en lugar de una IP pública.

Si tu escenario involucra orquestación con Azure ML/Foundry u otros, conviene habilitar esta opción para no bloquear esa integración al cerrar la red.

**Resumen de seguridad de red:** Puedes lograr que tu servicio Azure AI sea **tan privado como un servidor on-premises**, mediante VNets y Private Endpoints, integrándolo en tu arquitectura de red segura. Siempre prueba la conectividad tras aplicar cambios y ajusta DNS/configuraciones de clientes para que usen las rutas privadas.

**Preguntas de autoevaluación:**

1. Por defecto, un recurso de Azure AI recién creado tiene acceso de red desde:
   a. Cualquier origen en Internet (hasta que se restrinja).
   b. Solo la red virtual de Azure donde se creó.
   c. Ningún sitio, hay que habilitarlo manualmente.

2. ¿Qué opción permite **aislar completamente** tu recurso de Azure AI del Internet público, asegurando que solo través de tu red virtual se pueda acceder?
   a. Configurar el recurso en modo “Redes seleccionadas y puntos de conexión privados” y usar un **Punto de conexión privado**.
   b. Usar únicamente la autenticación por clave sin compartirla.
   c. Deshabilitar las claves de suscripción.

3. Activar la casilla de **“Permitir servicios de confianza de Azure”** en las configuraciones de red del recurso de Azure AI implica que:
   a. Algunos servicios Azure (ej. Azure ML, Search) podrán acceder incluso con la red cerrada, usando su identidad segura.
   b. Cualquiera con una suscripción Azure podrá acceder al recurso.
   c. Solo se permiten conexiones desde servicios locales, no desde Azure.
   
<br><br><br>
## Supervisión y monitoreo de los servicios de Azure AI

> 📌 **Concepto clave ➜** La **supervisión continua** de tus servicios de Azure AI te ayuda a **controlar costos**, detectar problemas de rendimiento y optimizar el uso. Azure proporciona herramientas para ver gastos, crear alertas, revisar métricas en tiempo real y habilitar logs detallados.

Una vez en funcionamiento, es crucial monitorear cómo se están comportando tus servicios de IA:

### Control de costos

Azure AI opera en un modelo **pay-as-you-go** (pagas por lo que consumes). Para evitar sorpresas o sobrecostos, utiliza las herramientas de Azure:

* **Nivel gratuito:** verifica si el servicio tiene un tier gratuito (muchos tienen límites mensuales gratis). Úsalo en desarrollo pero sé consciente de sus límites para no cruzarlos sin saber.
* **Calculadora de Precios:** Antes de usar intensivamente un servicio, ve a la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator) *(Azure > AI + Machine Learning > selecciona el servicio)*. Configura la región, el nivel (SKU) y una estimación de volumen (ej: 1 millón de caracteres/mes en Text Analytics, 5000 llamadas/mes, etc.). La calculadora te dará un **estimado de costo**. Puedes ajustar parámetros y también incluir múltiples servicios para ver el total. Exporta o guarda esta estimación para justificar presupuesto.
* **Análisis de costos en Azure Portal:** Durante el uso, en el portal Azure puedes ir a *Cost Management + Billing* -> *Cost Management* -> *Cost analysis*. Filtra por suscripción y por el servicio o recurso de Azure AI específico. Podrás ver el **gasto real acumulado**, incluso desglosado por servicio (p. ej. cuánto llevas gastado en Azure AI Language este mes). Usa filtros de tiempo para anticipar si a mitad de mes ya consumiste gran parte de tu presupuesto.
* **Documentación de precios:** Mantente actualizado con la página de precios oficial de Azure AI Services para conocer cambios de tarifas o nuevos planes.

### Creación de alertas de uso

Azure Monitor te permite definir **alertas personalizadas**. Por ejemplo, si el número de llamadas falla o si el gasto diario excede X:

* Ve al recurso Azure AI en el portal -> pestaña **Alertas** -> *Nueva regla de alerta*.
* Define el **Ámbito** (scope): puede ser el propio recurso o toda la suscripción si quieres alertar por costos en todos los AI.
* Define una **Condición**: Azure provee métricas por defecto, como *Transaction Count*, *Successful transactions*, *Failed transactions*, etc., según el servicio. También puedes alertar por **Cost** (hay integración con presupuesto).
* Ejemplos de condiciones: "*Más de 10 errores 5xx en 1 hora*" o "*El costo acumulado del servicio este mes > 100€* (requiere configurar un presupuesto en Cost Management)\*".
* Define **Acciones**: puedes enviar un email, un SMS, o invocar un webhook/Logic App para remediación. Por ejemplo, enviar correo al admin financiero si se supera cierto gasto.
* Ponle un **Nombre** y grábala. Las alertas corren cada pocos minutos y te notificarán si la condición se cumple.

Usando alertas, puedes enterarte rápidamente, por ejemplo, si de repente hay una alta tasa de errores (lo que podría indicar un problema en tu aplicación o un cambio en la API) en lugar de descubrirlo mucho después.

### Métricas en tiempo real

Azure Monitor recopila **métricas** estándar de los recursos de Azure AI. Algunas métricas típicas:

* **Número de solicitudes** (total count).
* **División de solicitudes exitosas vs fallidas**.
* **Latencia** (tiempo de respuesta promedio, p95, etc.).
* **Bytes de datos enviados/recibidos**.
* Dependiendo del servicio, métricas específicas (por ejemplo, en un recurso OpenAI, quizás #de tokens usados).

Para ver métricas:

* En el recurso, abre **Métricas** (en el portal).
* Selecciona la métrica de interés (p.ej. *Total Requests*).
* Puedes agregar varias métricas al mismo gráfico para compararlas (ej: exitosas vs fallidas).
* Ajusta el intervalo de tiempo y la agregación (promedio, suma, máximo…). Para tasas suele usarse suma o conteo por minuto.
* Puedes **fijar este gráfico en un panel (dashboard)** si lo vas a consultar frecuentemente: clic en el botón *Pin to dashboard*. Esto te permite crear un tablero personalizado con los gráficos clave de tus servicios (hasta 100 gráficos por tablero), útil para un vistazo general.

Ejemplo: podrías tener un panel con un gráfico de *Uso de API por hora*, otro de *Tasa de errores*, y otro de *Gasto acumulado este mes*. Así monitoreas salud y costo en un solo lugar.

### Registros de diagnóstico (logs)

Para análisis más profundo, habilita **Diagnostic Logs** en los recursos de Azure AI:

* Ve al recurso -> **Configuración de diagnóstico (Diagnostic settings)**.
* Crea una nueva configuración: dale un nombre (ej: "Log-Completo").
* Selecciona **categorías de log**. Según el servicio, puede haber logs de solicitud, de cumplimiento, etc. Por lo general incluye métricas de nivel de operación y quizá detalles de las peticiones (no el contenido en sí, sino metadata).
* Elige el **Destino** donde enviar los logs:

  * **Workspace de Log Analytics:** recomendado si quieres poder consultar logs con KQL (Kusto Query Language) en Azure Portal. Necesitas tener o crear un *Log Analytics Workspace*. Es ideal para centralizar logs de muchos servicios en un mismo lugar y hacer queries avanzadas.
  * **Cuenta de Azure Storage:** útil para archivar logs crudos a largo plazo o procesarlos externamente. *✅ Recomendación:* Si usas Storage, crea la cuenta en la **misma región** que el recurso Azure AI para minimizar latencia y costos egress.
  * **Event Hub:** si planeas integrar los logs con sistemas externos (SIEM de seguridad, o pipelines de Big Data), un EventHub puede retransmitir en vivo los eventos a esos sistemas.
* Guarda la configuración.

Tras habilitar, los eventos comenzarán a fluir en unos \~10 minutos.

**Uso de Log Analytics:** Si enviaste a un workspace, puedes ir al servicio Log Analytics y ejecutar consultas KQL. Por ejemplo:

```
AzureDiagnostics
| where ResourceType == "MICROSOFT.COGNITIVESERVICES/ACCOUNTS"
| where OperationName == "TextAnalysisSentiment" 
| summarize count() by bin(TimeGenerated, 1h)
```

Este query hipotético contaría cuántas operaciones de análisis de sentimiento se hicieron por hora. Puedes crear alertas a partir de logs también, o visualizar patrones de uso, clientes que llaman más, etc.

Supervisar también implica revisar **reportes de errores** de tu aplicación (¿está manejando bien las respuestas de IA?), y quizás hacer pruebas periódicas a la calidad del modelo (por ejemplo, con IA generativa, monitorear si las respuestas siguen siendo relevantes, etc.).

**Preguntas de autoevaluación:**

1. ¿Qué herramienta de Azure te permite **estimar el costo** de usar un servicio de Azure AI antes de implementarlo?
   a. Azure Cost Management (Análisis de costos)
   b. Azure Pricing Calculator (Calculadora de precios)
   c. Azure Advisor

2. Deseas recibir una **notificación si la tasa de errores** de tu servicio Azure AI (por ejemplo, llamadas que devuelven código 500) supera cierto umbral. ¿Qué funcionalidad usarías?
   a. Azure Monitor - **Reglas de alerta** basadas en métricas de errores.
   b. Un script manual que revise los logs de vez en cuando.
   c. No es posible, tendrías que descubrirlo manualmente.

3. ¿Cuál de los siguientes NO es un destino válido para enviar **registros de diagnóstico** de un servicio Azure AI?
   a. Azure Log Analytics
   b. Azure Storage Account
   c. GitHub Repos
   
<br><br><br>
## Implementación de servicios Azure AI en **contenedores**

> 📌 **Concepto clave ➜** Muchos servicios de Azure AI ofrecen **imágenes Docker** para ejecutarlos localmente o en el edge. Esto permite llevar la funcionalidad de IA **fuera de Azure** manteniendo un control total de los datos y la latencia, aunque requiere un recurso Azure para licenciamiento.

Microsoft provee contenedores Docker preconstruidos que encapsulan la misma funcionalidad que ciertos servicios de Azure AI en la nube. Usar contenedores tiene varias ventajas:

* **Portabilidad:** Puedes ejecutar el servicio en tu propio entorno: en un servidor on-premises, en un dispositivo en la frontera (*edge*), o incluso en otras nubes, sin depender de la conectividad continua a Azure para el procesamiento.
* **Baja latencia local:** Al tener el servicio corriendo cerca de donde están los datos o el usuario, evitas latencias de red hasta Azure. Por ejemplo, análisis de imágenes en una fábrica sin mandar cada imagen a un datacenter remoto.
* **Control de datos:** Los datos se procesan localmente en tu infraestructura, útil para escenarios con datos sensibles que no deban salir de cierto entorno (por regulación o política interna).
* **Escalabilidad personalizada:** Puedes levantar múltiples instancias del contenedor según tu necesidad, detrás de tu propio balanceador, etc., adaptándolo a tu arquitectura.

**¿Qué es un contenedor?** Es una unidad ligera que incluye la aplicación (en este caso, el servicio de IA) junto con **todas sus dependencias** (bibliotecas, runtime) en un paquete aislado. Usa el kernel del SO anfitrión pero mantiene su propio espacio, asegurando que el servicio correrá igual en cualquier host contenedor (Windows, Linux, etc.). Docker es la tecnología estándar para esto.

**Diferencia servicio en Azure vs contenedor:** Si usas el servicio en Azure, Microsoft se encarga de alojarlo en sus servidores; tú solo haces llamadas. En contenedor, **tú alojas el servicio** donde quieras, lo que te da flexibilidad pero también responsabilidad de mantener esa instancia corriendo.

### Obtención e implementación de contenedores

Microsoft publica las **imágenes de contenedor** en su registro de contenedores público **Microsoft Container Registry (MCR)**. Hay imágenes para muchas funcionalidades:

* En **Azure AI Language** (Text Analytics) hay contenedores separados para *Extracción de frases clave*, *Detección de idioma*, *Análisis de sentimiento*, *Reconocimiento de entidades (NER)*, *PII*, *Texto a salud*, *Resumen de texto*, etc.
  *Ejemplo:* la imagen `mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment` contiene el servicio de análisis de sentimiento.
* En **Azure AI Speech**, contenedores para *Speech to Text*, *Custom Speech to Text*, *Neural Text to Speech* (voz a texto neuronal), *Language detection en audio*, etc.
  *Ejemplo:* `mcr.microsoft.com/azure-cognitive-services/speechservices/speech-to-text` es reconocimiento de voz a texto.
* En **Vision**, contenedores para *Lectura OCR* (`vision/read`), *Análisis espacial* (`vision/spatial-analysis`), etc.
* **Traductor** también ofrece contenedor (`translator/text-translation`).
* **Content Safety:** al ser más reciente, podría incorporar contenedores en el futuro, pero inicialmente las imágenes son sobre todo para visión, lenguaje y voz.

> ℹ️ **Nota:** Algunas imágenes de contenedor pueden estar en **versión preliminar** y requerir solicitar acceso (por ejemplo, ciertos contenedores especializados). La documentación de *Container support for Azure Cognitive Services* mantiene la lista completa y actualizada de imágenes disponibles y sus estados.

**Requisitos para correr un contenedor:** Necesitas un ambiente con Docker instalado (puede ser tu máquina local para pruebas, o un servidor Linux/Windows con Docker, o plataformas como Azure Container Instances, Azure Kubernetes Service, etc.). También debes tener:

* **Una suscripción Azure y un recurso del servicio correspondiente aprovisionado**. *Sí, incluso ejecutándolo local, necesitas uno* — este se usa para facturación y para obtener la clave. Por ejemplo, para usar el contenedor de Text Analytics Sentiment, debes tener un recurso de Azure AI Language activo.
* **La clave y endpoint de ese recurso** a mano, para proporcionarlos al contenedor.

**Ejecutar el contenedor:** Se utiliza `docker run` con ciertos parámetros obligatorios que el contenedor espera:

* **ApiKey:** la clave del recurso Azure AI (clave de suscripción) – el contenedor la usará internamente para reportar uso a Azure (no para las peticiones locales).
* **Billing:** la URL del endpoint del recurso en Azure – indica al contenedor a qué recurso asociar el consumo para facturación.
* **ACCEPT\_EULA=Yes:** debes aceptar los términos de licencia de Microsoft para usar el contenedor. Esto se hace pasando esta variable de entorno con valor "Yes".

Por ejemplo, para levantar un contenedor de análisis de sentimiento podrías usar:

```bash
docker run -e ApiKey="<TU_CLAVE>" \
           -e Billing="<TU_ENDPOINT>" \
           -e ACCEPT_EULA=Yes \
           -p 5000:5000 \
           mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment:latest
```

Aquí estamos exponiendo el contenedor en el puerto 5000 local. Una vez corriendo, podrías hacer solicitudes HTTP a `http://localhost:5000/text/analytics/v3.1/sentiment` (por ejemplo) con tus datos, y el contenedor responderá similar a la API cloud.

**Nota:** Aunque las peticiones a tu contenedor **no requieren clave** (porque estás dentro de tu red confiada), el contenedor periódicamente **se comunica con Azure** para reportar métricas de uso usando la ApiKey/Billing que diste. De esta forma Azure sabe cuántas transacciones estás realizando y te cobra igual que si usaras el servicio en la nube. *(Esto ocurre tras bambalinas, normalmente cada pocos minutos envía un lote de conteo de peticiones.)*

**Uso seguro del contenedor:** Si bien tu endpoint local puede no requerir las claves, debes considerar protegerlo si es en producción (por ejemplo, con autenticación de tu propia aplicación o limitándolo a tu red interna), ya que cualquiera que acceda a ese puerto en tu red podría invocar el servicio.

**Parámetros opcionales:** Algunos contenedores permiten otros settings, como limitación de memoria, etc. Consulta la documentación de cada imagen.

**Importante:** Aunque uses contenedores offline, **mantén actualizado** el contenedor cuando salgan versiones nuevas (para recibir mejoras y parches de seguridad). Las imágenes tienen tags de versión; `:latest` suele ser la última estable.

### Limitaciones y consideraciones

* No todos los servicios Azure AI tienen versión en contenedor. Los que requieren mucha infraestructura (p.ej. Azure OpenAI GPT) *no* tienen contenedor (no puedes correr GPT-4 local, por ejemplo), por ahora solo servicios *cognitivos tradicionales*.
* Necesitas recursos de cómputo suficientes donde correrlos: por ejemplo, el contenedor de OCR con modelo pesado podría requerir varios GB de RAM.
* Monitoreo: los contenedores pueden exponer logs locales o métricas pero no envían datos detallados a Azure Monitor (solo contadores para billing). Así que deberás monitorearlos con herramientas locales (Docker logs, etc.) o integrarlos con tu sistema de contenedores (AKS, etc.) para health-checks.
* **⚠️ Importante:** Como se recalcó, **aun usando contenedores necesitas un recurso Azure** asociado. No es posible usar los contenedores indefinidamente sin conexión a Azure, porque requieren comunicarse para licenciamiento. Si el contenedor no puede reportar a Azure tras cierto tiempo, puede dejar de procesar (o Azure podría bloquear la clave).

**Preguntas de autoevaluación:**

1. ¿Cuál de las siguientes **NO** es una ventaja de utilizar contenedores de Azure AI?
   a. Ejecutar los servicios de IA en entornos sin conexión a internet o en el edge.
   b. Eliminar por completo la necesidad de una suscripción o recurso de Azure (no se necesita para nada Azure).
   c. Tener control sobre dónde se procesan los datos, manteniéndolos localmente.

2. Para **ejecutar un contenedor** de Azure AI Language en tu entorno local, necesitas proporcionar:
   a. La clave del recurso Azure AI correspondiente.
   b. El endpoint (URL) de tu recurso en Azure para facturación.
   c. Aceptar la licencia de uso del contenedor.
   d. **Todo lo anterior.**

3. **Verdadero o Falso:** Puedes usar los contenedores de Azure AI sin notificar a Azure, evitando cualquier cargo, siempre que no te conectes a internet.
   
<br><br><br>
## Uso responsable de IA con **Azure AI Content Safety**

> 📌 **Concepto clave ➜** **Azure AI Content Safety** es un servicio de moderación de contenido que **detecta texto e imágenes potencialmente ofensivos, violentos, de odio, sexuales o no deseados**, incluyendo intentos de ataque a modelos de IA. Ayuda a mantener interacciones seguras y respetuosas, reemplazando al antiguo Azure Content Moderator (retirado en 2024).

En los últimos años ha crecido exponencialmente el contenido generado por usuarios (en redes sociales, foros, chats) y también contenido producido por IA generativa. Esto trae riesgos de que se difunda material dañino o inapropiado. **Azure AI Content Safety** nace para abordar esos retos.

**¿Por qué es necesario un servicio de Content Safety?**

* 🚩 **Aumento de contenido dañino generado por usuarios:** Las plataformas reciben enormes volúmenes de posts, comentarios, imágenes, etc. Es inviable moderar todo manualmente; se requiere ayuda de IA para filtrar lenguaje soez, bullying, amenazas, etc.
* ⚖️ **Presiones normativas y legales:** Gobiernos y regulaciones exigen cada vez más controlar y remover ciertos contenidos (discurso de odio, terrorismo, abuso infantil…). Las empresas necesitan herramientas para cumplir estas normas a escala.
* 🔍 **Necesidad de transparencia en moderación:** Usuarios y organismos piden políticas claras. Un servicio de IA estandarizado permite aplicar reglas consistentes y explicar por qué algo fue marcado.
* 🎴 **Complejidad creciente (multimodal):** Ya no es solo moderar texto; ahora hay imágenes, videos, audio y combinaciones. Un comentario escrito sobre una foto puede requerir entender ambos para juzgar. Se necesitan sistemas que abarquen múltiples modalidades e identifiquen contexto.

**¿Dónde se usa Azure AI Content Safety?**
En cualquier aplicación donde los usuarios puedan *subir o generar contenido libremente*, o donde se utilicen modelos generativos que podrían producir texto/imágenes sensibles. Por ejemplo:

* Plataformas de **redes sociales y foros** (moderar publicaciones, comentarios, mensajes privados).
* **Aplicaciones de chat o mensajería** con posibilidad de compartir medios.
* Sitios web con **sección de comentarios** (noticias, blogs) o **reviews de productos** (e-commerce).
* **Juegos en línea** con chats de texto/voz, generación de emblemas o imágenes por usuarios.
* **Entornos educativos** en línea donde se quiera filtrar contenido inapropiado que alumnos puedan ingresar o ver.
* **Chatbots o asistentes virtuales con IA generativa** integrados en servicios al cliente, para asegurarse que no devuelvan respuestas ofensivas y que los *prompts* de los usuarios no induzcan a la IA a algo no deseado.
* En general, cualquier lugar donde la **imagen de marca** deba protegerse de asociación con contenido tóxico (por ejemplo, moderar foros oficiales de una empresa).

**Acceso y entorno:** Azure AI Content Safety está disponible:

* A través de **Azure AI Foundry** (como uno de los servicios integrados, con su propia sección *Safety + Security* y herramientas de “probar y ver código”).
* Mediante su propio portal especializado **Content Safety Studio**, pensado para que equipos de moderación prueben el servicio y ajusten configuraciones (por ejemplo, crear listas de bloqueo personalizadas).
* También cuenta con **API REST** y **SDKs** (actualmente C#, Python, Java, JavaScript) para integrarlo a aplicaciones de forma programática.

En Content Safety Studio se puede configurar umbrales de severidad, ver ejemplos de contenido moderado y hasta generar snippets de código listos para usar en tu app.

### Funcionalidades principales

Azure AI Content Safety ofrece varias funcionalidades para **protección de contenido de texto e imagen**:

**Para texto:**

* **Moderación de texto general:** Detecta en un texto las siguientes categorías de contenido prohibido: **violencia**, **odio**, **sexual** y **autolesión/suicidio**. Devuelve un nivel de **gravedad** para cada categoría (en una escala de 0 a 6, donde 0 es contenido seguro, 2 bajo, 4 medio, 6 alto). También da un resultado global *“Aceptado/Rechazado”* según los umbrales que configures. Por ejemplo, podría marcar un mensaje con nivel 6 en odio (lenguaje altamente ofensivo) -> Rechazado.
* **Prompt Shield (escudo de prompts):** Es una característica orientada a entradas a modelos de IA generativa. Detecta intentos de **ataque por inyección de prompt**, es decir, cuando un usuario introduce instrucciones maliciosas para engañar al modelo (por ejemplo, diciéndole que ignore sus filtros o revelando info sensitiva). Shield clasifica tales intentos para que puedas bloquear o sanitizar esas entradas antes de pasarlas al modelo.
* **Detección de material protegido (copyright):** Identifica si un texto contiene posiblemente contenido **protegido por copyright** como letras de canciones, párrafos de libros, recetas famosas, etc., que un usuario o IA podría estar publicando indebidamente.
* **Detección de “grounding” (fundamentación):** Pensando en salidas de LLMs, Content Safety puede analizar una respuesta generada y verificar si está **fundamentada en la fuente proporcionada** o si el modelo se desvió (alucinó) contenido no respaldado. Esto permite, por ejemplo, marcar respuestas de IA que suenen plausibles pero en realidad no estén basadas en la información fuente que se le dio. Incluso puede proporcionar *razonamiento* sobre por qué considera que no está fundamentada.

**Para imágenes:**

* **Moderación de imágenes:** Analiza imágenes en busca de contenido inaceptable en categorías similares: violencia (imágenes sangrientas, gore), sexual/nudity, autolesión (ej. imágenes promoviendo suicidio o uso de drogas), y odio (símbolos de odio, gestos ofensivos). Clasifica cada imagen con un nivel de severidad como **Seguro, Bajo, Medio o Alto** riesgo.
* **Moderación multimodal (bidireccional):** Combina la detección visual con OCR de texto dentro de la imagen. Esto mejora la precisión, ya que un meme dañino puede tener texto sobre una imagen. El servicio leerá el texto (ej: un insulto escrito en la imagen) y también evaluará la imagen en sí. La combinación permite captar casos que por separado podrían pasar.

**Soluciones personalizadas:**

* **Categorías personalizadas:** Además de las categorías estándar, puedes entrenar el sistema para **tus propias categorías** de contenido. Por ejemplo, quizás quieras filtrar *“spam”* o *“contenido político”* si tu caso de uso lo requiere, aunque no sean parte de las 4 categorías principales. Le proporcionas ejemplos de texto/imagen que caen en tu categoría custom (positivos y negativos) y el servicio aprenderá a marcarlos.
* **Mensajes del sistema de seguridad:** Son directrices o instrucciones que puedes configurar para moldear cómo la IA maneja contenido riesgoso. Por ejemplo, podrías configurar que ante cierto tipo de pregunta el asistente conteste con un mensaje específico (“Lo siento, no puedo ayudarte con eso”). Estos *system messages* funcionan como pautas integradas para la IA generativa cuando se usa en conjunto con Content Safety.

**Limitaciones actuales:**

* No es infalible: puede haber **falsos positivos** (marcar contenido inocuo como ofensivo) o **falsos negativos** (dejar pasar algo inapropiado). Por eso se recomienda calibrar los umbrales y **mantener supervisión humana**, especialmente en casos límite.
* Los modelos de moderación pueden tener sesgos o menor precisión en ciertos contextos culturales o jerga específica. Siempre es bueno evaluar su rendimiento con muestras de tu propio dominio.
* Content Safety es una herramienta de apoyo; en contenido crítico (ej. moderar millones de posts) suele emplearse como primer filtro automático, con operadores humanos revisando lo que la IA marca como dudoso o severo.
* **Es complementario a moderación humana:** Microsoft enfatiza que lo ideal es usarlo para **asistir a moderadores**, no para reemplazarlos al 100%. La combinación de IA + criterio humano logra el mejor balance entre cobertura y precisión.

De hecho, se definen métricas para evaluar la precisión de la moderación:

* *Verdadero Positivo (VP):* contenido efectivamente dañino que el sistema detectó correctamente.
* *Falso Positivo (FP):* contenido en realidad aceptable que fue marcado incorrectamente como dañino por la IA.
* *Verdadero Negativo (VN):* contenido limpio que pasó el filtro (correcto).
* *Falso Negativo (FN):* contenido inapropiado que el sistema no logró detectar (se escapó).
  Idealmente querríamos maximizar VP y VN, minimizando FP y FN; en la práctica hay que ajustar el umbral de tolerancia según prefieras pecar de bloquear de más o dejar pasar de más. Por ejemplo, una plataforma infantil tal vez prefiera algunos falsos positivos (bloquear cosas casi inocuas) con tal de no arriesgar falsos negativos de contenido adulto.

### Casos de uso clave de Content Safety

1. **Educación:** En entornos educativos en línea, Content Safety ayuda a **proteger a estudiantes y docentes** de contenido inapropiado. Por ejemplo, en foros de clase filtra lenguaje ofensivo o bullying. Si se usan asistentes de IA con alumnos, verifica que las respuestas estén fundamentadas (no desinformen) y evita *prompt injections* donde un alumno intente que el bot haga su tarea completa o genere respuestas inapropiadas.
2. **Redes sociales:** Plataformas tipo Twitter, Reddit, comentarios de blogs, etc. Content Safety puede **moderar texto e imágenes en tiempo real** antes de su publicación. Su soporte multilingüe y comprensión de matices (por ejemplo, insultos sutiles o jerga de odio) es clave para manejar la escala global y diversa, evitando toxicidad y frenando la propagación de desinformación o discurso de odio.
3. **Marcas/Empresas (Foros y atención al cliente):** Muchas empresas tienen **foros de soporte o comunidades de usuarios**. Content Safety previene que contenido ofensivo publicado allí **dañe la reputación** de la marca. También, si la empresa lanza un asistente conversacional público (basado en GPT, por ej.), el servicio protege al asistente para que no genere respuestas perjudiciales para la marca (por ejemplo, insultar a un cliente o soltar información no verificada).
4. **Comercio electrónico:** En sitios de e-commerce con **reseñas y comentarios de productos**, Content Safety puede detectar **reseñas falsas o spam**, lenguaje inapropiado en opiniones, o contenido no permitido (por ejemplo, fotos obscenas en reviews). Esto **protege la confianza** de los clientes en la plataforma y ayuda a cumplir normas (p.ej. quitar mensajes racistas).
5. **Juegos en línea:** Los juegos con interacción de usuarios (chat de texto/voz, creación de contenido como emblemas, nombres de usuario) pueden volverse tóxicos. Content Safety modera estos entornos **altamente visuales y dinámicos**: desde filtrar nombres ofensivos, hasta analizar mensajes de chat o imágenes subidas para avatares. En comunidades de juego masivas, esta moderación automática es fundamental para mantener un ambiente saludable.
6. **Servicios de IA generativa:** Si integras un modelo generativo (como GPT-4) en tu app, Content Safety puede **monitorear tanto las solicitudes de los usuarios (prompts) como las respuestas generadas**. Por ejemplo, si un usuario pide al modelo algo peligroso (cómo fabricar un arma), Content Safety lo detecta en el prompt y puedes denegar esa solicitud. O si el modelo devolviera sin querer un insulto o contenido sexual, puedes interceptarlo antes de mostrarlo. Esto añade una capa de seguridad alrededor del LLM.
7. **Sitios de noticias/comentarios públicos:** En portales de noticias con secciones de comentarios abiertos, es crucial moderar para evitar **discurso de odio, comentarios incendiarios o desinformación** en temas sensibles. Content Safety ayuda a señalar esos contenidos para revisión o bloqueo, manteniendo un espacio de debate más seguro y civil.
8. **Casos personalizados:** Industrias con requisitos propios pueden entrenar Content Safety para casos especiales. Ejemplo: en un foro médico, quizá quieran filtrar consejos peligrosos (pseudo-ciencia) además de lo típico. O en una comunidad de literatura, podrían querer bloquear *spoilers* de libros. Al permitir modelos custom, Azure AI Content Safety se puede ajustar a **comunidades específicas** o entornos muy regulados (financiero, gubernamental, etc.).

En conclusión, Azure AI Content Safety es una herramienta poderosa para **automatizar la moderación** y **proteger a usuarios y empresas** del contenido no deseado o nocivo. Usada con criterio (ajustando umbrales, combinando con revisión humana para casos críticos) puede escalar donde la moderación manual no llega, creando experiencias en línea más seguras.

**Preguntas de autoevaluación:**

1. ¿Cuál de las siguientes **NO** es una categoría de contenido que Azure AI Content Safety evalúa explícitamente?
   a. Contenido violento
   b. Lenguaje de odio
   c. Publicidad/Spam

2. El mecanismo **Prompt Shield** de Content Safety está diseñado para:
   a. Detectar intentos de usuarios de manipular a modelos generativos con instrucciones maliciosas (prompt injection).
   b. Bloquear automáticamente cualquier prompt largo.
   c. Añadir autenticación de dos factores a las solicitudes de la API.

3. Una limitación importante de Azure AI Content Safety es:
   a. Puede incurrir en falsos positivos o negativos, por lo que se recomienda supervisión humana complementaria.
   b. Solo funciona para contenido en inglés y no admite otros idiomas.
   c. No se integra con otros servicios de Azure y debe usarse aislado.

   
<br><br><br>
## Glosario de términos clave

* **IA generativa:** Tipo de inteligencia artificial capaz de **crear contenido original** (texto, imágenes, audio, etc.) a partir de indicaciones, en lugar de solo analizar datos existentes. *Ejemplo:* ChatGPT generando una respuesta única a una pregunta.

* **Agente de IA:** Programa de IA (a menudo usando IA generativa) que **actúa de forma autónoma** para cumplir objetivos o responder interactivamente. Puede tomar decisiones y acciones sin supervisión continua.

* **Visión por computadora:** Campo de la IA enfocado en **interpretar contenido visual** (fotos, vídeo). Incluye tareas como detección de objetos, reconocimiento facial, OCR, etc., imitando la forma en que la vista humana percibe e interpreta imágenes.

* **OCR:** Siglas de *Optical Character Recognition*, tecnología para **reconocer y extraer texto de imágenes o documentos escaneados**. Los servicios de **Inteligencia de Documentos** usan OCR avanzado para leer recibos, facturas, etc.

* **LLM (Large Language Model):** *Gran modelo de lenguaje* entrenado con enormes cantidades de texto, capaz de **entender y generar lenguaje natural**. Ejemplos son GPT-3/GPT-4. Son la base de muchas funciones de Azure OpenAI (chatbots, completación de texto).

* **Azure AI Foundry:** Plataforma unificada de Azure para **desarrollar proyectos de IA de forma colaborativa**. Proporciona organización mediante **Centros** y **Proyectos**, recursos pre-configurados y herramientas integradas (catálogo de modelos, playgrounds, etc.) para agilizar soluciones de IA.

* **Centro (Hub) de Foundry:** Contenedor de nivel superior en Azure AI Foundry que **centraliza recursos compartidos, seguridad y configuraciones** comunes a múltiples proyectos de IA. Todos los proyectos dentro de un centro heredan esos recursos (servicios de Azure AI, almacenamiento, etc.).

* **Proyecto de Foundry:** Unidad de trabajo en Azure AI Foundry dentro de un centro, donde un equipo colabora en una **solución de IA específica**. Agrupa datasets, modelos y resultados particulares de ese caso de uso, usando los recursos que el centro le provee.

* **Azure Key Vault:** Servicio de Azure para **almacenar de forma segura claves, secretos y certificados**. Permite guardar, por ejemplo, las claves de servicios Azure AI y recuperarlas desde las apps mediante autenticación, evitando exponer secretos directamente.

* **Identidad administrada:** Identidad de Azure AD que Azure gestiona automáticamente para un servicio (p. ej., una VM o función). Se usa para **autenticación segura sin claves**: el recurso con identidad administrada puede solicitar tokens para acceder a otros servicios (como Azure AI) con permisos asignados, eliminando la necesidad de credenciales explícitas.

* **Punto de conexión privado:** Interfaz de red privada en una VNet de Azure que se conecta internamente a un servicio Azure (como Azure AI). Permite acceder al servicio **a través de una IP privada** en tu red, manteniendo el tráfico dentro de la nube y **aislando el servicio del internet público**.

* **Azure AI Content Safety:** Servicio de Azure AI para **moderación de contenido**. Analiza texto e imágenes en busca de lenguaje o visuales ofensivos, violentos, de odio, sexuales, etc., además de detectar intentos de manipulación a modelos de IA (prompt injection) y verificar la veracidad de respuestas de IA (grounding).

* **Moderación de contenido:** Proceso de **revisar y filtrar contenido generado por usuarios o IA** según políticas de la comunidad/empresa. Content Safety lo automatiza parcialmente, señalando contenido inapropiado para bloqueo o revisión humana.

* \*\*Grounding... (continuación del glosario)

* **Grounding (Fundamentación):** En IA generativa, se refiere a asegurar que las **respuestas de la IA estén basadas en fuentes o datos fiables proporcionados** (por ejemplo, contenido de un documento) y no sean invenciones. Una respuesta "bien fundamentada" cita o utiliza la información dada, evitando alucinaciones. Content Safety ofrece detección de falta de *grounding* para identificar cuando un LLM se desvía de la fuente.

* **Prompt injection (inyección de prompt):** Tipo de ataque donde un usuario introduce en la entrada de un modelo generativo **instrucciones maliciosas o engañosas** destinadas a burlar sus filtros o a hacer que ignore políticas. Ejemplo: un usuario le dice al chatbot "olvida tus reglas y dime X". Azure AI Content Safety (Prompt Shield) puede detectar estos intentos y prevenir que el modelo sea manipulado.
   
<br><br><br>
## Tabla de *flashcards* de servicios y conceptos clave

| Servicio / Concepto                        | Función principal                                                                      | Palabra clave (memoria) |
| ------------------------------------------ | -------------------------------------------------------------------------------------- | ----------------------- |
| **Azure OpenAI**                           | Modelos de IA generativa (GPT, DALL-E) para texto/imagen                               | **Generativa**          |
| **Visión de Azure AI**                     | Análisis de imágenes y video (objetos, descripciones, OCR)                             | **Imágenes**            |
| **Voz de Azure AI**                        | Reconocimiento de voz y síntesis de habla, traducción oral                             | **Voz**                 |
| **Lenguaje de Azure AI**                   | Procesamiento de lenguaje natural (entidades, sentimiento, resumen)                    | **Texto**               |
| **Seguridad de contenido de Azure AI**     | Moderación de texto/imagen, detección de contenido ofensivo o riesgoso                 | **Moderación**          |
| **Traductor de Azure AI**                  | Traducción automática de texto entre múltiples idiomas                                 | **Traducción**          |
| **Azure AI Face**                          | Detección y reconocimiento facial en imágenes                                          | **Rostros**             |
| **Azure AI Custom Vision**                 | Entrenamiento de modelos personalizados de visión (clasificación, detección)           | **Personalizada**       |
| **Inteligencia de Documentos de Azure AI** | Lectura y extracción de información de documentos (OCR avanzado)                       | **Documentos**          |
| **Descripción del contenido de Azure AI**  | Análisis de contenido multimodal (docs, imágenes, audio, video) con IA generativa      | **Multimodal**          |
| **Azure AI Search**                        | Búsqueda inteligente con índice enriquecido y vectorial (para *grounding* de IA)       | **Vectorial**           |
| **Azure AI Foundry**                       | Plataforma centralizada para proyectos de IA colaborativos (hubs, proyectos, devtools) | **Colaborativa**        |
