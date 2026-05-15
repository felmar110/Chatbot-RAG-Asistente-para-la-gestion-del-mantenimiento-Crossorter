# Chatbot RAG: Asistente para la gestion del mantenimiento de Crossorter

## Descripción del Proyecto

Este proyecto implementa un chatbot de Generación Aumentada por Recuperación (RAG) diseñado para asistir en la resolución de dudas sobre el plan de mantenimiento de las bandas transportadoras de un sistema de clasificación de mercancía automatizado (Crossorter). El chatbot utiliza un `vector_store` (embeddings) para recuperar información relevante de documentos PDF y Excel, y luego genera respuestas coherentes y basadas en el contexto utilizando la API de Gemini. En caso de no encontrar información relevante, el chatbot está configurado para indicar explícitamente que no tiene la respuesta en sus fuentes, evitando "inventar" información.

## Características Principales

*   **Recuperación de Información (RAG):** Utiliza embeddings de Gemini para buscar y recuperar fragmentos de texto (`chunks`) relevantes de documentos preprocesados (PDFs y Excels).
*   **Generación de Respuestas Contextuales:** Emplea un modelo generativo de Gemini (`gemini-2.5-flash`) para sintetizar respuestas basadas en la información recuperada.
*   **Manejo de Respuestas sin Información:** Si no se encuentran documentos relevantes para una consulta, el chatbot informa que no puede responder con la información proporcionada.
*   **Interfaz Amigable:** Desarrollado con Gradio para una interacción sencilla a través de una interfaz web.
*   **Autocontenido para Despliegue:** El `app.py` incluye la lógica para cargar o, si es necesario, generar el `vector_store` automáticamente al iniciar el Space, facilitando el despliegue.

## Tecnologías Utilizadas

*   **Google Gemini API:** Para la generación de embeddings (`gemini-embedding-2`) y el modelo de lenguaje generativo (`gemini-2.5-flash`).
*   **Gradio:** Para construir la interfaz de usuario del chatbot.
*   **`pypdf`:** Para la extracción de texto de documentos PDF.
*   **`pandas` y `openpyxl`:** Para la lectura y procesamiento de documentos Excel.
*   **`numpy` y `scikit-learn`:** Para operaciones numéricas y cálculo de similitud de coseno.
*   **Python:** Lenguaje de programación principal.
*   **Hugging Face Spaces:** Plataforma de despliegue.

## Estructura de Archivos Esencial

Para que la aplicación funcione correctamente, tu Hugging Face Space debe tener la siguiente estructura de directorios y archivos:

```
mi-awesome-space/
├── app.py                     # El código principal de la aplicación
└── data/                      # Directorio para tus documentos y el vector_store
    ├── tu_documento_1.pdf
    ├── tu_documento_2.xlsx
    └── vector_store.pkl       # Almacén de embeddings (generado o subido)
```

## Configuración (API Key)

Para utilizar la API de Gemini, necesitas una clave API. Sigue estos pasos:

1.  **Obtén tu API Key:** Si no tienes una, créala en [Google AI Studio](https://aistudio.google.com/app/apikey).
2.  **Configura el Secreto en Hugging Face Space:** En la configuración de tu Hugging Face Space, ve a la sección "Secrets" y añade una nueva variable secreta con el nombre `Key_Gemini` y tu clave API como valor. El `app.py` está configurado para buscar este nombre de secreto (`os.getenv('Key_Gemini')`).

## Instalación y Ejecución Local (Opcional)

Si deseas ejecutar el chatbot localmente para desarrollo o pruebas, sigue estos pasos:

1.  **Clona el Repositorio (si aplica) o crea `app.py`:**
    ```bash
    git clone <URL_DE_TU_REPOSITORIO_DE_HF>
    cd <nombre-de-tu-repositorio>
    # O crea un archivo app.py y pega el código
    ```
2.  **Crea el directorio `data` y coloca tus documentos:**
    ```bash
    mkdir data
    # Copia tus PDFs y Excels a la carpeta 'data'
    ```
3.  **Instala las dependencias:**
    ```bash
    pip install -r requirements.txt # Si tienes un requirements.txt
    # O instala manualmente:
    pip install google-generativeai gradio pypdf pandas openpyxl numpy scikit-learn
    ```
4.  **Configura tu API Key:**
    Crea una variable de entorno `Key_Gemini` con tu clave API antes de ejecutar la aplicación. Por ejemplo (en Linux/macOS):
    ```bash
    export Key_Gemini='TU_CLAVE_API_DE_GEMINI'
    ```
    En Windows (CMD):
    ```bash
    set Key_Gemini=TU_CLAVE_API_DE_GEMINI
    ```
    En Windows (PowerShell):
    ```powershell
    $env:Key_Gemini='TU_CLAVE_API_DE_GEMINI'
    ```
5.  **Ejecuta la aplicación:**
    ```bash
    python app.py
    ```
    La aplicación se iniciará y te proporcionará una URL local donde podrás acceder a la interfaz de Gradio.

## Despliegue en Hugging Face Spaces

1.  **Crea un nuevo Space:** Ve a [Hugging Face Spaces](https://huggingface.co/spaces) y crea un nuevo Space.
2.  **Sube los Archivos:** Sube `app.py` a la raíz de tu Space. Crea la carpeta `data` y sube tus documentos PDF/Excel a `data/`. Si ya tienes un `vector_store.pkl` completo, súbelo también a `data/`. De lo contrario, el `app.py` lo generará en el primer arranque.
3.  **Configura los Secretos:** Asegúrate de que tu `Key_Gemini` esté configurada como un secreto en tu Space.
4.  **Espera el Despliegue:** Hugging Face Space detectará tu `app.py` y desplegará automáticamente la aplicación. El primer arranque puede ser más lento si necesita generar los embeddings.

## Link a la App Desplegada

https://huggingface.co/spaces/Felmar110/Chatbot-Crossorter

## Uso de la Aplicación

Simplemente escribe tus preguntas en el cuadro de texto del chat y presiona `Enter` o el botón de enviar. El chatbot recuperará la información más relevante de tus documentos y generará una respuesta. Si no encuentra información, te lo hará saber.

## Ejemplos de Preguntas

*   `¿Qué repuesto es el más usado para las reparaciones?`
*   `¿Qué motores tuvieron fuga de aceite el último trimestre del año?`
*   `¿Cuál fue el último mantenimiento o reparación realizada y quién la realizó?`

## Capturas de Pantalla
<img width="1600" height="792" alt="WhatsApp Image 2026-05-14 at 10 49 21 PM" src="https://github.com/user-attachments/assets/026c6de9-a5a1-49e8-a461-15402e887fd6" />
<img width="1280" height="660" alt="WhatsApp Image 2026-05-15 at 12 00 45 AM" src="https://github.com/user-attachments/assets/3bc060c4-74e3-47cf-bb61-45eb4f09800f" />
<img width="2288" height="811" alt="WhatsApp Image 2026-05-15 at 12 02 00 AM" src="https://github.com/user-attachments/assets/35791f0c-3183-4b59-a715-a32136888067" />

