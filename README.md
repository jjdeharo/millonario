# ¿Quién Quiere Ser Millonario? - Juego de Trivia

Este proyecto es una implementación web del popular juego de trivia "¿Quién Quiere Ser Millonario?". Permite cargar preguntas desde un archivo JSON externo, jugar con comodines y disfrutar de una experiencia interactiva.

## Características

* **Carga de Preguntas Dinámica**: Las preguntas se cargan desde un archivo JSON alojado externamente, lo que facilita la creación y personalización de los cuestionarios.
* **Múltiples Niveles de Dificultad**: El juego está diseñado para soportar preguntas con diferentes niveles de dificultad, incrementando el desafío progresivamente.
* **Comodines**: Incluye los comodines clásicos:
    * 50:50: Elimina dos respuestas incorrectas.
    * Llamada a un Amigo: Simula una llamada que sugiere una respuesta (generalmente la correcta).
    * Voto del Público: Muestra un gráfico simulado de cómo votaría el público.
* **Escala de Premios**: Visualiza el progreso del jugador a través de una escala de premios.
* **Interfaz Bilingüe**: Soporte para Español (es) y Catalán (ca), con detección automática del idioma del navegador.
* **Renderizado de LaTeX**: Soporte para mostrar fórmulas matemáticas utilizando MathJax.
* **Personalización del Jugador**: Permite al jugador introducir su nombre.
* **Responsive Design**: Adaptado para una buena visualización en diferentes tamaños de pantalla.

## ¿Cómo Funciona el Programa?

El juego está construido con HTML, CSS y JavaScript puro. No requiere un backend complejo, ya que las preguntas se cargan desde un archivo JSON especificado por el usuario mediante una URL.

1.  **Inicio**: Al cargar la página (`index.html`), el juego inicializa la interfaz y el sistema de traducción.
2.  **Carga de Preguntas**:
    * El usuario introduce la URL de un archivo JSON que contiene las preguntas.
    * El script de JavaScript (`<script>` dentro de `index.html`) realiza una petición `fetch` para obtener el archivo JSON.
    * Valida el JSON para asegurar que tiene la estructura correcta y el contenido esperado.
    * Si el JSON es válido, se oculta el cargador de JSON y se habilita el botón para empezar el juego.
3.  **Inicio del Juego**:
    * Al pulsar "Empezar juego", se pide al jugador que introduzca su nombre (si es la primera vez).
    * Se seleccionan las preguntas para la primera ronda según la dificultad (`easy`).
4.  **Desarrollo del Juego**:
    * Se muestra la pregunta actual y las cuatro opciones.
    * El jugador selecciona una opción.
    * Se verifica si la respuesta es correcta.
    * Si es correcta, el jugador avanza en la escala de premios y pasa a la siguiente pregunta.
    * Si es incorrecta, el juego termina y se muestra la puntuación final.
    * El jugador puede usar los comodines una vez por partida.
5.  **Rondas Siguientes**: Al completar una ronda (o perder), el jugador puede optar por "Reiniciar juego", lo que iniciará una nueva ronda con preguntas del siguiente nivel de dificultad, si están disponibles.
6.  **Fin de Partidas**: Si se completan todas las dificultades o no hay suficientes preguntas para una nueva ronda, se informa al jugador, ofreciendo la opción de reiniciar todo el progreso (lo que permitiría volver a jugar todas las preguntas o cargar un nuevo JSON).

## Creación del Archivo JSON de Preguntas

Para que el juego funcione, necesitas crear un archivo JSON con una estructura específica.

### Estructura del JSON

```json
{
  "tema": "Nombre del tema de las preguntas",
  "preguntas": [
    {
      "question": "Texto de la pregunta. Puede incluir LaTeX como <span class="math-inline">E\=mc^2</span>.",
      "options": {
        "A": "Opción A. Puede ser texto o LaTeX, ej: <span class="math-inline">\\\\alpha</span>",
        "B": "Opción B. Puede ser texto o LaTeX, ej: <span class="math-inline">\\\\beta</span>",
        "C": "Opción C. Puede ser texto o LaTeX, ej: <span class="math-inline">\\\\gamma</span>",
        "D": "Opción D. Puede ser texto o LaTeX, ej: <span class="math-inline">\\\\delta</span>"
      },
      "correct": "A",
      "difficulty": "easy"
    }
    // ... más preguntas
  ]
}
