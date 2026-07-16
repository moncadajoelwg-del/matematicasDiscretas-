# Parte A (Fundamentos y Tipos): Árboles en Teoría de Grafos

Los **árboles son una de las subclases de grafos más importantes y utilizadas en las ciencias de la computación**. Su estructura jerárquica y la ausencia de redundancia los convierten en la herramienta perfecta para organizar información de manera eficiente y restrictiva.

---

## 1. Definiciones Fundamentales

Un **árbol** es un grafo conexo que no contiene ningún ciclo o circuito. En términos matemáticos abstractos:

*   **Conexo:** Significa que siempre existe al menos un camino para viajar entre cualquier par de vértices; no hay nodos aislados ni subgrupos separados.
*   **Acíclico:** Significa que es imposible salir de un vértice, recorrer una serie de aristas distintas y regresar al mismo vértice de origen. 

Si un grafo es **acíclico pero no es conexo** (es decir, está compuesto por varios árboles separados), se le conoce técnicamente como un **Bosque**.

---

## 2. Propiedades Matemáticas de los Árboles

Para cualquier grafo simple $G = (V, E)$ con $n$ vértices, las siguientes afirmaciones son equivalentes y definen las propiedades rígidas de un árbol:

1.  **Relación Vértices-Aristas:** Si un árbol tiene $n$ vértices, tiene exactamente **$n - 1$ aristas**. Si agregas una sola arista más, creas un ciclo obligatoriamente. Si quitas una arista, el grafo deja de ser conexo.
2.  **Caminos Únicos:** Entre cualquier par de vértices de un árbol existe **exactamente un único camino simple**. No hay rutas alternativas.
3.  **Vértices Hoja:** Todo árbol finito con al menos dos vértices contiene, como mínimo, **dos vértices de grado 1** (llamados hojas o nodos terminales).
4.  **Conectividad Mínima:** Los árboles son los grafos conexos con el menor número posible de aristas. Eliminar cualquier arista fragmenta el grafo en dos componentes disjuntas.

---

## 3. Caracterización de Árboles Enraizados

Un **árbol enraizado** es un árbol en el cual uno de sus vértices ha sido designado formalmente como la **raíz**. Esta simple asignación introduce un sentido de dirección y jerarquía (relaciones de arriba hacia abajo), transformando las aristas en arcos dirigidos que se alejan de la raíz.

A partir de la raíz, se despliega una terminología genealógica específica:

*   **Padre (Parent):** El nodo inmediatamente superior conectado a un nodo específico en la ruta hacia la raíz.
*   **Hijo (Child):** Cualquier nodo inmediatamente inferior que tiene como ancestro directo al nodo padre.
*   **Hermanos (Siblings):** Nodos que comparten exactamente el mismo padre.
*   **Ancestros / Descendientes:** Los ancestros son todos los nodos en la ruta desde el nodo actual hasta la raíz. Los descendientes son todos los nodos que tienen al nodo actual como ancestro.
*   **Nivel o Profundidad:** El número de aristas que separan a un nodo de la raíz. La raíz está en el nivel 0.
*   **Altura:** El nivel máximo o más profundo que alcanza cualquier hoja dentro del árbol.

### Árboles $m$-arios y Árboles Binarios
*   Un árbol enraizado es **$m$-ario** si cada nodo interno (que no es hoja) tiene como máximo $m$ hijos.
*   Un árbol es **$m$-ario completo** si cada nodo interno tiene exactamente $m$ hijos.
*   El caso más famoso en computación es el **Árbol Binario** ($m = 2$), donde cada nodo puede tener, a lo sumo, dos hijos (tradicionalmente llamados *hijo izquierdo* e *hijo derecho*).

---

## 4. Aplicaciones Principales en Computación

Los árboles no son solo conceptos teóricos; sostienen la infraestructura del software moderno a través de las siguientes aplicaciones:

*   **Árboles de Búsqueda Binaria (BST):** Estructuras donde para cada nodo, los valores a la izquierda son menores y a la derecha son mayores. Permiten realizar búsquedas, inserciones y eliminaciones en tiempo logarítmico $O(\log n)$, superando drásticamente a las listas lineales.
*   **Sistemas de Archivos:** Las carpetas y archivos de cualquier sistema operativo (Windows, Linux, macOS) se organizan como un árbol enraizado, donde el directorio raíz (`C:` o `/`) es el origen de toda la jerarquía.
*   **Árboles de Expresión:** Utilizados por los compiladores e intérpretes de lenguajes de programación para descomponer y evaluar operaciones matemáticas y lógicas (por ejemplo, analizar la sintaxis de una ecuación).
*   **Algoritmos de Enrutamiento (Spanning Trees):** En redes de computadoras, el protocolo STP (*Spanning Tree Protocol*) desactiva enlaces redundantes en una red física para construir un árbol de expansión libre de bucles, evitando el colapso de la transmisión de datos.
*   **Compresión de Datos (Árbol de Huffman):** Un algoritmo que asigna códigos de longitud variable a los caracteres basándose en su frecuencia, optimizando el espacio al guardar archivos (como los formatos ZIP o JPEG).
# Parte B (Optimización y Búsqueda): Árboles, Prefijos y Estructuras de Datos

La eficiencia en el almacenamiento, transmisión y recuperación de información digital depende de optimizaciones estructurales basadas en propiedades métricas de los árboles enraizados.

---

## 1. Análisis de la Longitud de Paseo en Árboles

La **longitud de paseo** (o longitud de camino) es una métrica fundamental para evaluar la eficiencia de un árbol en computación, ya que mide el costo de acceso a sus nodos.

### Longitud de Paseo Interna ($I$)
Es la suma de los niveles (profundidades) de todos los **nodos internos** (no hojas) del árbol con respecto a la raíz. 
* Si un árbol tiene su raíz en el nivel 0 y dos hijos internos en el nivel 1, su contribución inicial es $0 + 1 + 1 = 2$.

### Longitud de Paseo Externa ($E$)
Es la suma de los niveles de todos los **nodos hoja** (terminales) del árbol. 

### El Teorema de Longitud de Paseo para Árboles Binarios
En cualquier árbol binario con exactamente $n$ nodos internos, existe una relación matemática estricta entre ambas longitudes expresada mediante la fórmula:
$$E = I + 2n$$

### Longitud de Paseo Ponderada ($W$)
En aplicaciones reales (como la compresión de datos), los nodos hoja no tienen el mismo valor. A cada hoja $i$ se le asigna un peso $w_i$ (que representa su frecuencia o probabilidad de aparición). La longitud de paseo ponderada se calcula como:
$$W = \sum_{i=1}^{k} w_i \cdot l_i$$
Donde $l_i$ es el nivel (longitud del camino desde la raíz) de la hoja $i$. **Optimizar un árbol consiste en minimizar este valor $W$**, logrando que los nodos con mayor peso (más frecuentes) queden en los niveles más altos (más cerca de la raíz).

---

## 2. Códigos de Prefijos y Códigos de Huffman

### Fundamentos de los Códigos de Prefijos
Un código de prefijo es un sistema de codificación donde **ninguna palabra clave (secuencia de bits) es el prefijo de otra**. 
* Si la letra **A** se codifica como `0`, ninguna otra letra puede empezar con `0` (por ejemplo, **B** no puede ser `01`). 
* **Ventaja computacional:** Permite una decodificación instantánea de izquierda a derecha sin ambigüedad y sin requerir caracteres separadores. Se representan de forma natural mediante árboles binarios enraizados, donde las hojas son los caracteres y los caminos hacia la izquierda añaden un `0` y hacia la derecha un `1`.

### Construcción del Algoritmo de Huffman
El código de Huffman es un método de compresión de datos sin pérdida que construye un árbol binario óptimo (con la mínima longitud de paseo ponderada) de abajo hacia arriba (*bottom-up*).

#### Algoritmo de Construcción Paso a Paso:
1.  **Inicialización:** Crear un nodo hoja para cada carácter del alfabeto, asignándole su frecuencia de aparición como peso. Todos los nodos entran a una cola de prioridad.
2.  **Combinación Iterativa:** Mientras quede más de un nodo en la cola:
    *   Extraer los dos nodos con las frecuencias más bajas ($n_1$ y $n_2$).
    *   Crear un nuevo nodo interno cuyo peso sea la suma de las frecuencias de $n_1$ y $n_2$.
    *   Asignar $n_1$ como hijo izquierdo y $n_2$ como hijo derecho de este nuevo nodo.
    *   Insertar el nuevo nodo interno de regreso en la cola de prioridad.
3.  **Asignación de Códigos:** Cuando queda un solo nodo, este se convierte en la raíz del árbol de Huffman. Se recorre el árbol desde la raíz hasta cada hoja asignando `0` para giros a la izquierda y `1` para giros a la derecha.

---

## 3. Lógica Matemática detrás de los Árboles de Búsqueda Binaria (ABB)

Un Árbol de Búsqueda Binaria es una estructura de datos diseñada para optimizar operaciones de búsqueda dinámicas basándose en una propiedad de ordenamiento estricta.

### La Propiedad Esencial del ABB
Para cualquier nodo intermedio $X$ dentro del árbol, se debe cumplir rigurosamente que:
1. Todos los valores almacenados en el **subárbol izquierdo** de $X$ deben ser estrictamente **menores** que el valor del nodo $X$.
2. Todos los valores almacenados en el **subárbol derecho** de $X$ deben ser estrictamente **mayores** o iguales que el valor del nodo $X$.

$$\forall \, y \in \text{Subárbol Izquierdo}(X) \implies \text{Valor}(y) < \text{Valor}(X)$$
$$\forall \, z \in \text{Subárbol Derecho}(X) \implies \text{Valor}(z) > \text{Valor}(X)$$

# Parte C (Recorridos - Ejercicios Prácticos): Navegación en Árboles

Los recorridos de árboles son operaciones algorítmicas estructuradas que visitan cada nodo exactamente una vez. A diferencia de las estructuras lineales (como listas o arreglos), los árboles admiten diferentes rutas de exploración debido a su naturaleza bidimensional y jerárquica.

---

## 1. Explicación Analítica de los Recorridos Fundamentales

En un árbol binario, el orden de visita se define a partir de tres elementos clave: el **Nodo Raíz o Actual (\(R\))**, el **Subárbol Izquierdo (\(I\))** y el **Subárbol Derecho (\(D\))**. La distinción entre los tres recorridos principales radica exclusivamente en **cuándo se procesa la raíz** con respecto a sus hijos.

Los tres algoritmos se ejecutan de manera recursiva:

### Preorden (Pre-order: \(R \to I \to D\))
La raíz se procesa **antes** que los subárboles.
1. Visitar el nodo actual (Raíz).
2. Recorrer el subárbol izquierdo en Preorden.
3. Recorrer el subárbol derecho en Preorden.
*   **Caso de uso:** Copiar la estructura exacta de un árbol o evaluar expresiones en notación polaca (prefija).

### Inorden (In-order: \(I \to R \to D\))
La raíz se procesa **en medio** de ambos subárboles.
1. Recorrer el subárbol izquierdo en Inorden.
2. Visitar el nodo actual (Raíz).
3. Recorrer el subárbol derecho en Inorden.
*   **Caso de uso:** En los Árboles de Búsqueda Binaria (ABB), este recorrido extrae los elementos de forma **estrictamente ordenada de menor a mayor**.

### Postorden (Post-order: \(I \to D \to R\))
La raíz se procesa **después** de haber agotado ambos subárboles.
1. Recorrer el subárbol izquierdo en Postorden.
2. Recorrer el subárbol derecho en Postorden.
3. Visitar el nodo actual (Raíz).
*   **Caso de uso:** Liberar memoria (eliminar nodos sin dejar huérfanos) o resolver operaciones matemáticas en calculadoras de notación polaca inversa (posfija).

---

## 2. Resolución de Ejercicio Práctico Paso a Paso

Para demostrar la mecánica matemática y algorítmica de los recorridos, utilizaremos el siguiente árbol binario de caracteres:

```text
         [M]
        /   \
     [F]     [S]
     / \       \
   [B] [H]     [X]
```

### Ejercicio 1: Resolución del Recorrido Preorden ($R \to I \to D$)
Avanzamos procesando inmediatamente cada raíz que tocamos de arriba hacia abajo y de izquierda a derecha.

1.  **Raíz principal:** Registramos **M**. Pasamos al subárbol izquierdo.
2.  **Nodo F:** Es una raíz secundaria. Registramos **F**. Pasamos a su izquierda.
3.  **Nodo B:** Es una raíz hoja. Registramos **B**. Como no tiene hijos, la recursión regresa a **F** y salta a su derecha.
4.  **Nodo H:** Es una hoja. Registramos **H**. El subárbol izquierdo de **M** se ha completado. Pasamos a su subárbol derecho.
5.  **Nodo S:** Es una raíz secundaria. Registramos **S**. No tiene hijo izquierdo, saltamos directamente a su derecha.
6.  **Nodo X:** Es una hoja. Registramos **X**.

*   **Resultado Final Preorden:** `M -> F -> B -> H -> S -> X`

---

### Ejercicio 2: Resolución del Recorrido Inorden ($I \to R \to D$)
Bajamos hasta el nodo situado más a la izquierda antes de registrar cualquier elemento.

1.  Desde **M**, bajamos a **F**, y luego al extremo izquierdo **B**.
2.  **Nodo B:** No tiene hijo izquierdo, procesamos su raíz: **B**. No tiene hijo derecho, subimos al padre.
3.  **Nodo F:** Ya procesamos su lado izquierdo completo. Procesamos su raíz: **F**. Pasamos a su derecha.
4.  **Nodo H:** Bajamos a **H**. No tiene izquierda, procesamos raíz: **H**. Subimos al nodo inicial.
5.  **Nodo M:** El bloque izquierdo está terminado. Procesamos la raíz principal: **M**. Pasamos al bloque derecho.
6.  Desde **M** vamos a **S**. El subárbol izquierdo de **S** está vacío, por lo que procesamos inmediatamente su raíz: **S**. Pasamos a su derecha.
7.  **Nodo X:** Vamos al extremo derecho. No tiene izquierda, procesamos raíz: **X**.

*   **Resultado Final Inorden:** `B -> F -> H -> M -> S -> X`
*   *Nota analítica:* Al ser este un Árbol de Búsqueda Binaria válido, notarás que las letras quedaron ordenadas alfabéticamente de manera perfecta.

---

### Ejercicio 3: Resolución del Recorrido Postorden ($I \to D \to R$)
No podemos registrar un nodo padre hasta haber procesado e impreso de manera absoluta todos sus hijos correspondientes.

1.  Bajamos por el extremo izquierdo pasando por **M** y **F** hasta llegar a la hoja **B**.
2.  **Nodo B:** Al no tener hijos, se procesa a sí mismo como raíz: **B**. Volvemos a **F**, pero no podemos registrarlo aún; debemos ir primero a su hijo derecho.
3.  **Nodo H:** Es una hoja sin descendientes. Se procesa a sí mismo: **H**.
4.  **Nodo F:** Con sus dos hijos procesados (`B` y `H`), el algoritmo finalmente tiene permiso de registrar la raíz: **F**.
5.  Volvemos a **M**, pero su bloque derecho está pendiente. Saltamos a **S**.
6.  Desde **S**, intentamos ir a la izquierda (vacío), luego vamos a la derecha hasta la hoja **X**.
7.  **Nodo X:** Hoja terminal. Se registra a sí mismo: **X**.
8.  **Nodo S:** Con su descendencia resuelta, registramos la raíz secundaria: **S**.
9.  **Nodo M:** Con todo el subárbol izquierdo (`B, H, F`) y el derecho (`X, S`) completados, registramos la gran raíz del sistema: **M**.

*   **Resultado Final Postorden:** `B -> H -> F -> X -> S -> M`


### Comportamiento Computacional y Degeneración
*   **Búsqueda Eficiente:** Gracias a esta lógica, el algoritmo de búsqueda emula una búsqueda binaria. En cada nodo, se compara el valor buscado: si es menor, se descarta todo el subárbol derecho; si es mayor, se descarta el izquierdo.
*   **Complejidad Ideal:** En un árbol balanceado (donde la altura es mínima), el tiempo de búsqueda, inserción y eliminación es **$O(\log n)$**.
*   **El Problema de la Degeneración (Peor Caso):** Si los datos se insertan en orden estrictamente ascendente (ej. 1, 2, 3, 4), el árbol pierde su estructura ramificada y se convierte en una lista enlazada lineal. En este estado "degenereado", la altura del árbol pasa a ser $n$ y la complejidad de las operaciones colapsa a un ineficiente **$O(n)$**. Esto justifica la existencia de variantes auto-balanceables como los árboles AVL o Rojo-Negro.
