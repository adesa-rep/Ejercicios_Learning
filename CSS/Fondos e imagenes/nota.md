### **Por qué es necesario hacer que ocupe espacio como un bloque?**

Hacer que el pseudo-elemento ocupe espacio como un bloque con **`display: block;`** es crucial en este caso porque estamos usando **`padding-top`** para crear una altura proporcional al ancho del contenedor. Aquí está el porqué:

- **Qué pasa sin `display: block;`?**
  Sin **`display: block;`**, el pseudo-elemento **`::before`** no ocuparía espacio como un bloque en el flujo del diseño. Por defecto, los pseudo-elementos tienen **`display: inline`**, lo cual:
  1. Haría que **`padding-top`** no afectara la altura del pseudo-elemento porque los elementos en línea no responden igual al relleno vertical.
  2. Esto significa que el pseudo-elemento no generaría una altura proporcional al ancho, rompiendo el "aspect ratio" que queremos lograr.
  - **Resumen**
    - Si eliminamos **`display: block;`**, el pseudo-elemento no tendría efecto visual porque:
      1. Seguiría siendo un elemento en línea (como texto normal).
      2. El **`padding-top`** no aumentaría la altura del contenedor padre.
    - Con **`display: block;`**, el pseudo-elemento:
      1. Se comporta como un bloque, ocupando todo el ancho disponible.
      2. El **`padding-top`** ahora genera un espacio vertical basado en el ancho, "empujando" la altura del contenedor.
- **¿Por qué necesitamos un "aspect ratio"?**
  El truco para mantener proporciones fijas (1:1, 16:9, etc.) sin especificar directamente la altura de un elemento se basa en el uso de **`padding-top`** o **`padding-bottom`**, porque **el relleno es relativo al ancho del contenedor**.
  - **`padding-top`** calcula un porcentaje en función del ancho del contenedor, pero solo funciona si el pseudo-elemento tiene un comportamiento de bloque, ya que los bloques permiten que el relleno "empuje" el tamaño del contenedor hacia abajo.

### **¿Por qué usar un pseudo-elemento en lugar del contenedor principal?**

Podríamos aplicar directamente el **`padding-top`** al contenedor `.width`, pero usar un pseudo-elemento tiene ventajas:

- **Evita interferir con el contenido interno.**
  - El pseudo-elemento solo existe para definir el espacio vertical y no afecta otros estilos del contenedor.
- **Permite superponer contenido.**
  - El contenido (como el texto) puede posicionarse encima del pseudo-elemento usando `position: absolute` sin conflictos.
  - **como funciona esto?**
    - **El pseudo-elemento (`::before`) crea el espacio:**
      - El pseudo-elemento genera un espacio (altura) dentro del contenedor, que define su tamaño usando `padding-top`.
      - Esto no afecta el contenido interno del contenedor, porque el pseudo-elemento no interfiere con el flujo del diseño.
    - **El contenido se posiciona con `position: absolute`:**
      - El contenedor principal tiene `position: relative`.
      - Esto hace que todos los elementos con `position: absolute` dentro del contenedor se posicionen **en relación al contenedor**, no al pseudo-elemento.
      - Así, podemos centrar o mover el contenido visible libremente sin interferir con la altura del pseudo-elemento.
