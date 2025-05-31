# ¿Quién quiere ser millonario? - juego de trivia

Este proyecto es una versión web del famoso concurso “¿Quién quiere ser millonario?”. Permite cargar preguntas desde un archivo JSON externo, usar comodines clásicos y disfrutar de una experiencia interactiva.

## Características

- **Carga dinámica de preguntas**. El juego lee las preguntas desde un archivo JSON alojado en línea, lo que simplifica la creación y personalización de los cuestionarios.  
- **Varios niveles de dificultad**. Las preguntas pueden clasificarse como `easy`, `medium` o `hard`, aumentando el reto de forma progresiva.  
- **Comodines integrados**  
  - **50:50** — elimina dos respuestas incorrectas.  
  - **Llamada a un amigo** — simula una llamada que sugiere (normalmente) la respuesta correcta.  
  - **Voto del público** — muestra un gráfico con el voto simulado del público.  
- **Escala de premios**. El progreso se refleja en una barra con los importes alcanzados.  
- **Interfaz bilingüe**. Soporta español (`es`) y catalán (`ca`) con detección automática del idioma del navegador.  
- **Renderizado LaTeX**. Las fórmulas matemáticas se muestran mediante MathJax.  
- **Nombre del jugador**. El usuario puede introducir su nombre antes de empezar.  
- **Diseño adaptable**. Funciona correctamente en móviles, tabletas y pantallas de escritorio.

## ¿Cómo funciona el programa?

El juego está desarrollado en HTML, CSS y JavaScript puro; no requiere backend.

1. **Inicio**  
   Al abrir `index.html`, se inicializan la interfaz y el sistema de traducción.  
2. **Carga de preguntas**  
   - El usuario introduce la URL del archivo JSON.  
   - Un `fetch` obtiene ese archivo y comprueba que su estructura sea válida.  
   - Si todo es correcto, se habilita el botón **Empezar juego**.  
3. **Inicio del juego**  
   - El jugador escribe su nombre (solo la primera vez).  
   - Se cargan las preguntas `easy`.  
4. **Turno de preguntas**  
   - Se muestra una pregunta con cuatro opciones.  
   - El jugador elige una respuesta.  
   - Si acierta, avanza en la escala; si falla, la partida termina y se muestra la puntuación.  
   - Cada comodín puede usarse una sola vez por partida.  
5. **Rondas siguientes**  
   Tras terminar una ronda (victoria o fallo), el jugador puede **Reiniciar juego**. Si hay preguntas `medium` o `hard`, se emplearán en la nueva partida.  
6. **Fin de las partidas**  
   Si se terminan todas las preguntas disponibles, se ofrece reiniciar todo el progreso o cargar un nuevo JSON.

## Creación del archivo JSON de preguntas

El juego necesita un archivo con la estructura siguiente:

```json
{
  "tema": "Nombre del tema",
  "preguntas": [
    {
      "question": "Texto de la pregunta. Puede incluir LaTeX como \\(E = mc^2\\).",
      "options": {
        "A": "Opción A (ej. \\(\\alpha\\))",
        "B": "Opción B (ej. \\(\\beta\\))",
        "C": "Opción C (ej. \\(\\gamma\\))",
        "D": "Opción D (ej. \\(\\delta\\))"
      },
      "correct": "A",
      "difficulty": "easy"
    }
    // añade más objetos separados por comas
  ]
}
