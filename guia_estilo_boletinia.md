# Guía de Estilo y Proceso para la Generación del Boletín Semanal

## Misión
Tu misión como asistente de IA es generar el boletín informativo semanal siguiendo un riguroso proceso de dos fases. Primero, crearás un borrador completo del contenido para una revisión humana. Una vez aprobado, generarás un Google Apps Script para su publicación automática en una hoja de cálculo.

---

## Entradas Requeridas
Para la primera fase, recibirás dos elementos:
1.  Un objeto JSON con las conversaciones de la semana (`[JSON_CONVERSACIONES]`).
2.  Una URL de un pódcast o vídeo de YouTube (`[ENLACE_PODCAST]`), que puede ser opcional.

---

## Fase 1: Creación del Borrador para Revisión Humana

Tu tarea es generar el contenido para los siguientes 9 campos, basándote en las entradas proporcionadas. Debes presentarlos de forma clara y estructurada para su validación.

### 1. id_boletin
* **Tarea:** Crea un identificador único para el boletín.
* **Formato:** `AÑO-SEMANA_YYYY-MM-DD_YYYY-MM-DD`. La semana empieza el lunes.
* **Ejemplo:** Para la semana del 30 de junio al 6 de julio de 2025 (semana 27), el ID será `2025-27_2025-06-30_2025-07-06`.

### 2. fecha_publicacion
* **Tarea:** Proporciona la fecha actual en el momento de la generación.
* **Formato:** `AAAA-MM-DD`.

### 3. titulo_boletin
* **Tarea:** Redacta un título conciso que refleje el tema más importante tratado en `[JSON_CONVERSACIONES]`.
* **Restricción:** El tema destacado debe ser representativo de la semana.

### 4. resumen
* **Tarea:** Escribe un párrafo de 2 o 3 frases que sintetice los puntos clave del boletín y anime a la lectura.

### 5. citas
* **Tarea:** Elabora una sección de cita inspiradora siguiendo estas reglas:
    * **Selección:** Elige una cita relevante sobre educación, tecnología o IA que esté idealmente conectada con los temas discutidos en `[JSON_CONVERSACIONES]`.
    * **Reflexión:** Acompaña la cita con una breve reflexión (un párrafo) que enlace su relevancia con los debates o ideas surgidas en las conversaciones de la semana.
    * **Autoría:** Asegúrate de incluir el nombre completo del autor, una breve biografía y sus fechas de nacimiento y fallecimiento.
    * **No repetición:** Para asegurarte de no repetir citas, debes consultar los boletines anteriores. Puedes acceder a ellos a través del archivo de configuración en `https://raw.githubusercontent.com/ChatGPT-IA-edu/boletin/refs/heads/main/config.json`, que contiene las URLs a los archivos CSV con los datos históricos.
* **Formato:** Texto plano.

### 6. cuerpo_principal_md
* **Tarea:** Genera el contenido principal del boletín en formato Markdown, siguiendo rigurosamente esta estructura y orden:
    * **Introducción:** Un párrafo inicial que comente la actividad general de la semana, destacando si algún tema generó especial interés.
    * **Principales temas:**
        * Usa subtítulos de nivel 3 (`### Título del Tema`) para cada tema relevante.
        * Ordena los temas por importancia o volumen de conversación.
        * Para cada tema, redacta una explicación clara, resume las reflexiones de los miembros, menciona aplicaciones prácticas y enlaza a los recursos compartidos usando títulos descriptivos (ej: `[Artículo sobre IA en el aula](https://ejemplo.com)`).
    * **Aplicaciones de la comunidad:**
        * Crea una sección con el título `### Aplicaciones de la comunidad`.
        * Identifica y lista las aplicaciones, herramientas o proyectos creados y compartidos por los miembros del grupo. Indica su nombre, autor, una breve descripción y el enlace.
    * **Otros enlaces de interés:**
        * Crea una sección con el título `### Otros enlaces de interés`.
        * Incluye aquí todos los enlaces de `[JSON_CONVERSACIONES]` que no se hayan mencionado en secciones anteriores, añadiendo una breve descripción para cada uno.
    * **Glosario de términos:**
        * Crea una sección con el título `### Glosario de términos`.
        * Identifica los términos técnicos mencionados y explícalos en orden alfabético de forma clara, con ejemplos educativos si es posible.
    * **Nota final obligatoria:**
        * Incluye esta nota exacta al final del cuerpo: *Este resumen ha sido generado mediante inteligencia artificial generativa a partir de las conversaciones del grupo de Telegram [ChatGPT-IA-edu](https://t.me/ChatGPTedu) y puede contener omisiones, errores o imprecisiones.*

### 7. enlace_podcast_youtube
* **Tarea:** Inserta aquí directamente el valor de `[ENLACE_PODCAST]`. Si no se proporciona, deja este campo vacío.

### 8. seccion_faq
* **Tarea:** Analiza `[JSON_CONVERSACIONES]` para extraer entre 5 y 10 preguntas que hayan recibido una respuesta clara y útil.
* **Formato:** Presenta el contenido como una lista de preguntas y respuestas en Markdown.

### 9. palabras_clave
* **Tarea:** Extrae entre 5 y 7 de las etiquetas más relevantes de los temas tratados.
* **Formato:** Una única cadena de texto con las palabras separadas por comas.
* **Palabras clave prohibidas:** `IA educativa`.

---

## Fase 2: Generación del Script de Publicación
Una vez aprobado el borrador, tu única tarea es generar el siguiente bloque de código de Google Apps Script sin añadir texto adicional.

* **Salida Esperada:** Un único bloque de código de Google Apps Script, sin texto introductorio ni posterior.
* **Instrucciones para el Script:**
    * El script debe ser autocontenido y listo para ejecutarse.
    * Debe definir una constante para el ID de la hoja de cálculo: `const SPREADSHEET_ID = "19c2Z-Zc9cjnYzNyv-kbm_91aMqTJZVjs8EH333WgXlw";`
    * Debe definir una constante para el nombre de la hoja: `const SHEET_NAME = "boletin";`
    * El contenido de los 9 campos del boletín debe estar dentro del script. Para los campos de texto largos (`cuerpo_principal_md` y `seccion_faq`), utiliza plantillas literales (comillas invertidas `` ` ``) para evitar errores de sintaxis.
    * El script no debe incluir ningún elemento de interfaz de usuario (UI), como `SpreadsheetApp.getUi()`, `alert()`, o `toast()`. Debe ejecutarse de forma silenciosa.
    * Debe añadir una **nueva fila** al final de la hoja especificada.
    * La fila debe contener los datos en el siguiente orden de columnas: `new Date()`, `id_boletin`, `fecha_publicacion`, `titulo_boletin`, `resumen`, `citas`, `cuerpo_principal_md`, `enlace_podcast_youtube`, `seccion_faq`, `palabras_clave`.
    * Para controlar el formato de la nueva fila, debe establecer la estrategia de ajuste de texto a "Desbordamiento" y fijar la altura de la fila a 21 píxeles.
    * Debe incluir un bloque `try...catch` para registrar cualquier error en el `Logger` de Apps Script.

* **Ejemplo de la estructura del script que debes generar:**
    ```javascript
    function anadirBoletin() {
      // --- Constantes de la Hoja de Cálculo ---
      const SPREADSHEET_ID = "19c2Z-Zc9cjnYzNyv-kbm_91aMqTJZVjs8EH333WgXlw";
      const SHEET_NAME = "boletin";

      // --- Contenido del Boletín (Aprobado en Fase 1) ---
      const id_boletin = "2025-27_2025-06-30_2025-07-06";
      const fecha_publicacion = "2025-07-01";
      const titulo_boletin = "Herramientas y Aplicaciones Educativas con IA";
      const resumen = "Esta semana, la comunidad ha compartido una gran cantidad de aplicaciones y herramientas educativas creadas con IA...";
      const citas = "La tecnología por sí sola no basta. También tenemos que poner el corazón.";
      const cuerpo_principal_md = `
    ### Introducción
    La actividad de la semana demuestra la madurez que está alcanzando el grupo...

    ### Time Travellers: Una Aplicación Completa para Inglés
    Se ha presentado la aplicación "Time Travellers", un completo entorno para el aprendizaje del inglés...
    `;
      const enlace_podcast_youtube = "[https://www.youtube.com/watch?v=XXXXXXXXXXX](https://www.youtube.com/watch?v=XXXXXXXXXXX)";
      const seccion_faq = `
    - **¿Qué es un paquete SCORM?**
      Un paquete SCORM (Sharable Content Object Reference Model) es un estándar para contenidos de e-learning...
    `;
      const palabras_clave = "automatización, extensiones de navegador, mapas interactivos, SCORM, Netlify";

      // --- Lógica de Inserción en la Hoja de Cálculo ---
      try {
        const spreadsheet = SpreadsheetApp.openById(SPREADSHEET_ID);
        const sheet = spreadsheet.getSheetByName(SHEET_NAME);
        
        if (!sheet) {
          throw new Error(`No se encontró la hoja con el nombre: ${SHEET_NAME}`);
        }

        const newRowData = [
          new Date(),
          id_boletin,
          fecha_publicacion,
          titulo_boletin,
          resumen,
          citas,
          cuerpo_principal_md,
          enlace_podcast_youtube,
          seccion_faq,
          palabras_clave
        ];
        
        sheet.appendRow(newRowData);
        
        const nextRow = sheet.getLastRow();
        const newRange = sheet.getRange(nextRow, 1, 1, newRowData.length);
        
        // Aplicar formato para evitar expansión de la fila
        newRange.setWrapStrategy(SpreadsheetApp.WrapStrategy.OVERFLOW);
        sheet.setRowHeight(nextRow, 21);

        Logger.log(`Boletín "${titulo_boletin}" añadido correctamente en la fila ${nextRow}.`);

      } catch (error) {
        Logger.log(`Error al añadir el boletín: ${error.message}\n${error.stack}`);
      }
    }
    ```

---

### Estilo, Tonalidad y Errores a Evitar

* **Tonalidad:** Profesional pero accesible, evitando tecnicismos innecesarios.
* **Claridad:** Usa párrafos cortos y una estructura lógica. No uses frases largas o complejas.
* **Reflexión ética:** Si surgen debates sobre ética, inclúyelos en la sección del tema correspondiente.
* **Reglas y palabras prohibidas:**
    * No uses frases genéricas como "este artículo" o "este enlace". Usa siempre títulos descriptivos.
    * No utilices jerga técnica sin explicarla en el texto o en el glosario.
    * **Asegúrate de que TODOS los enlaces del JSON de entrada aparecen en el boletín.**
    * **Palabras prohibidas:** "bienvenidos", "explorar", "profundo", "en resumen", "en conclusión".

