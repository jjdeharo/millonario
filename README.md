# ¿Quién quiere ser millonario?

Este proyecto, creado a partir de una bifurcación del original de [Ernesto Boixader](https://github.com/eboixader/magnitunid), es una versión web del famoso concurso “¿Quién quiere ser millonario?”. Permite cargar preguntas desde un archivo JSON externo, usar comodines clásicos y disfrutar de una experiencia interactiva.

## Características

* **Carga dinámica de preguntas**. El juego lee las preguntas desde un archivo JSON alojado en línea, lo que simplifica la creación y personalización de los cuestionarios.
* **Varios niveles de dificultad**. Las preguntas pueden clasificarse como `easy`, `medium`, `hard`, `very-hard` o `expert`, aumentando el reto de forma progresiva.
* **Comodines integrados**

  * **50:50** — elimina dos respuestas incorrectas.
  * **Llamada a un amigo** — simula una llamada que sugiere (normalmente) la respuesta correcta.
  * **Voto del público** — muestra un gráfico con el voto simulado del público.
* **Escala de premios**. El progreso se refleja en una barra con los importes alcanzados.
* **Interfaz bilingüe**. Soporta español (`es`) y catalán (`ca`) con detección automática del idioma del navegador.
* **Renderizado LaTeX**. Las fórmulas matemáticas se muestran mediante MathJax.
* **Nombre del jugador**. El usuario puede introducir su nombre antes de empezar.
* **Diseño adaptable**. Funciona correctamente en móviles, tabletas y pantallas de escritorio.

## ¿Cómo funciona el programa?

El juego está desarrollado en HTML, CSS y JavaScript puro.

1. **Inicio**
   Al abrir `index.html`, se inicializan la interfaz y el sistema de traducción.
2. **Carga de preguntas**

   * Si no se han especificado preguntas en la misma URL (véase más abajo) el usuario introduce la URL del archivo JSON.
   * Se obtiene ese archivo y comprueba que su estructura sea válida.
   * Si todo es correcto, se habilita el botón **Empezar juego**.
3. **Inicio del juego**

   * El jugador escribe su nombre (solo la primera vez).
   * Se cargan las preguntas `easy`.
4. **Turno de preguntas**

   * Se muestra una pregunta con cuatro opciones.
   * El jugador elige una respuesta.
   * Si acierta, avanza en la escala; si falla, la partida termina y se muestra la puntuación.
   * Cada comodín puede usarse una sola vez por partida.
5. **Rondas siguientes**
   Tras terminar una ronda (victoria o fallo), el jugador puede **Reiniciar juego**. Si hay preguntas `medium`, `hard`, `very-hard` o `expert`, se emplearán en la nueva partida.
6. **Fin de las partidas**
   Si se terminan todas las preguntas disponibles, se ofrece reiniciar todo el progreso o cargar un nuevo JSON.

## Creación del archivo JSON de preguntas

El juego necesita un archivo con la estructura siguiente.

```json
{
  "tema": "Nombre del tema",
  "preguntas": [
    {
      "question": "Texto de la pregunta. Puede incluir LaTeX como \(E = mc^2\).",
      "options": {
        "A": "Opción A (ej. \(\alpha\))",
        "B": "Opción B (ej. \(\beta\))",
        "C": "Opción C (ej. \(\gamma\))",
        "D": "Opción D (ej. \(\delta\))"
      },
      "correct": "A",
      "difficulty": "easy"
    }
  ]
}
```

---

## Prompt para generar JSON de preguntas – ¿Quién quiere ser millonario?
Utiliza tu IA favorita para crear las preguntas con el prompt que hay a continuación.

````markdown
### Paso 1 – preguntar al usuario

Antes de generar nada, **pregunta al usuario el tema** sobre el que quiere las preguntas.  
Ejemplo:  
> ¿Sobre qué tema quieres que genere las preguntas tipo test? (Ejemplo: cinemática, derivadas, genética…)

### Paso 2 – generar el JSON cuando el usuario dé el tema

#### Estructura requerida

```json
{
  "tema": "Nombre del tema de las preguntas",
  "preguntas": [
    {
      "question": "Texto de la pregunta",
      "options": {
        "A": "Primera opción",
        "B": "Segunda opción",
        "C": "Tercera opción",
        "D": "Cuarta opción"
      },
      "correct": "A",
      "difficulty": "easy"
    }
  ]
}
```

#### Especificaciones obligatorias

1. **`tema`** refleja exactamente el tema indicado.
2. **`preguntas`** contiene **60 preguntas** en un único archivo:  
   - 12 `easy`  
   - 12 `medium`  
   - 12 `hard`  
   - 12 `very-hard`  
   - 12 `expert`
3. Para cada pregunta:  
   - `question`: enunciado claro y directo.  
   - `options`: cuatro claves `A`, `B`, `C`, `D` con respuestas distintas.  
   - `correct`: letra única (`A`, `B`, `C` o `D`) distribuida al azar y de forma equilibrada en todo el conjunto.  
   - `difficulty`: uno de los cinco niveles indicados.

#### Criterios por dificultad

- **easy**: definiciones o cálculos directos.  
- **medium**: interpretación o aplicación básica.  
- **hard**: relaciones técnicas o fórmulas con contexto.  
- **very-hard**: uso riguroso de fórmulas o propiedades menos habituales.  
- **expert**: formulaciones específicas, combinadas o contraejemplos.

#### Formato adicional

- Emplea **LaTeX** en `$…$` o `$$…$$` para fórmulas.  
- Usa unidades SI correctas (`$m/s^2$`, `$kg·m/s$`, `$N·m$`, etc.).  
- Varía los enunciados:  
  - ¿Cuál es…?  
  - ¿Qué se entiende por…?  
  - ¿Cómo se calcula…?  
  - ¿Cuál de las siguientes afirmaciones es falsa?

#### Validaciones obligatorias

- No repitas preguntas ni opciones textualmente.  
- Solo una opción correcta por pregunta.  
- Distribuye aleatoriamente la respuesta correcta entre A, B, C y D.  
- Entrega **todo el JSON en una sola respuesta**, sin fragmentar.  
- **No incluyas comentarios** dentro del JSON; cualquier texto que empiece con `//`, `#` o `/*` lo invalidaría.
````

## Cómo subir el JSON a GitHub Gist y obtener la URL
Una vez tengas las preguntas las podrás subir al servicio Gist de GitHub que, de forma gratuita, permite tener archivos de texto accesibles desde todo Internet, lo que es ideal para alojar las preguntas.

1. Entra en: [https://gist.github.com](https://gist.github.com)
2. Accede con tu cuenta de GitHub (si no tienes una, puedes crearla gratuitamente).
3. Rellena el formulario:

   * En el primer campo, escribe un nombre para el archivo, como `preguntas.json`
   * En el cuadro grande, pega todas las preguntas generadas (en formato JSON)
   * Marca la opción **Create public gist** (gisto público)
   * Haz clic en **Create public gist**
     ![image](https://github.com/user-attachments/assets/97f64fcb-6b16-49eb-b41d-428baf806b76)

4. Una vez creado:

   * Pulsa en el botón **Raw** para ver solo el contenido del archivo
   * Copia la dirección (URL) que aparece en el navegador: es la que usarás en el juego
     ![image](https://github.com/user-attachments/assets/9936acb7-5d4c-4400-9a76-1f5023ca9fae)


## ¿Cómo usar la URL del JSON en el juego?

Una vez hayas subido el archivo de preguntas a GitHub Gist y tengas la dirección (la URL que aparece al hacer clic en el botón **Raw**), puedes usarla directamente para abrir el juego con esas preguntas precargadas.

Solo tienes que añadir la dirección de tu archivo JSON al final de la URL del juego, usando `?json=` o `?preguntas=`.

### Ejemplo

Supón que tu archivo de preguntas está en:

```
https://gist.githubusercontent.com/usuario/hash/raw/preguntas.json
```

Y que el juego está en:

```
https://jjdeharo.github.io/millonario
```

Entonces puedes abrir directamente el juego con las preguntas cargadas así:

```
https://jjdeharo.github.io/millonario?preguntas=https://gist.githubusercontent.com/usuario/hash/raw/preguntas.json
```

Cuando lo hagas, el juego usará automáticamente ese archivo y mostrará las preguntas sin que tengas que pegar nada manualmente.

Aquí tienes dos juegos funcionales:
- [Derivadas de funciones](https://jjdeharo.github.io/millonario/?preguntas=https://gist.githubusercontent.com/jjdeharo/518ee579638b23a7073b5c0b529f5194/raw/bb45b5cad5866e47e22714ceb5ee22241811d077/derivadas.json).
- [Literatura universal](https://jjdeharo.github.io/millonario/?preguntas=https://gist.githubusercontent.com/jjdeharo/fd5eba4b4cd9d752800e61756adaa508/raw/ad07b2bb181ad0b21130284085e66df83f93523e/literatura.json).
