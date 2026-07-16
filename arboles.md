# Resumen: Árboles en Teoría de Grafos y Estructuras de Datos

## 1. Definiciones Fundamentales
Un **árbol** es un grafo conexo y acíclico.
*   **Conexo:** Existe un camino entre cualquier par de vértices.
*   **Acíclico:** No contiene ciclos ni circuitos.
*   **Bosque:** Grafo acíclico pero no conexo (conjunto de árboles).

---

## 2. Propiedades Matemáticas
Para un grafo con $n$ vértices:
*   **Aristas:** Tiene exactamente $n - 1$ aristas.
*   **Caminos Únicos:** Existe un único camino simple entre cualquier par de nodos.
*   **Hojas:** Todo árbol con $n \ge 2$ tiene al menos dos vértices de grado 1.
*   **Conectividad Mínima:** Quitar cualquier arista desconceta el grafo.

---

## 3. Árboles Enraizados y Jerarquía
Tienen un nodo fijo llamado **raíz** (nivel 0). Establecen relaciones jerárquicas:
*   **Padre / Hijo:** Nodos superiores e inferiores directamente conectados.
*   **Hermanos:** Nodos con el mismo padre.
*   **Ancestros / Descendientes:** Nodos en la ruta hacia la raíz / nodos derivados.
*   **Altura:** Nivel máximo que alcanza una hoja.
*   **Árbol $m$-ario:** Cada nodo interno tiene como máximo $m$ hijos (completo si tiene exactamente $m$).
*   **Árbol Binario:** Caso donde $m = 2$ (hijo izquierdo e hijo derecho).

---

## 4. Aplicaciones en Computación
*   **Árboles de Búsqueda Binaria (BST):** Búsquedas rápidas en tiempo logarítmico $O(\log n)$.
*   **Sistemas de Archivos:** Organización de directorios y carpetas (raíz `C:` o `/`).
*   **Árboles de Expresión:** Evaluación y análisis sintáctico de operaciones en compiladores.
*   **Spanning Tree Protocol (STP):** Desactiva enlaces redundantes en redes para evitar bucles.
*   **Compresión de Datos:** Reducción de espacio mediante códigos variables (Huffman).

---

## 5. Métricas de Eficiencia (Longitud de Paseo)
*   **Interna ($I$):** Suma de los niveles de todos los nodos internos.
*   **Externa ($E$):** Suma de los niveles de todos los nodos hoja.
*   **Teorema Binario:** En árboles binarios con $n$ nodos internos: $E = I + 2n$.
*   **Ponderada ($W$):** $W = \sum w_i \cdot l_i$, donde $w_i$ es el peso (frecuencia) y $l_i$ el nivel de la hoja. Optimizar implica minimizar $W$.

---

## 6. Códigos de Prefijos y de Huffman
*   **Código de Prefijo:** Ninguna palabra clave es prefijo de otra. Permite decodificación instantánea.
*   **Algoritmo de Huffman:** Compresión sin pérdida que minimiza la longitud ponderada ($W$).
*   **Construcción:** 
    1. Introduce los caracteres en una cola de prioridad según su frecuencia.
    2. Combina iterativamente los dos nodos de menor peso en un nuevo nodo padre con la suma de sus frecuencias.
    3. Al quedar un solo nodo (raíz), asigna `0` a la izquierda y `1` a la derecha *(Texto interrumpido en el original)* para definir los códigos binarios.
ión y eliminación es **$O(\log n)$**.
*   **El Problema de la Degeneración (Peor Caso):** Si los datos se insertan en orden estrictamente ascendente (ej. 1, 2, 3, 4), el árbol pierde su estructura ramificada y se convierte en una lista enlazada lineal. En este estado "degenereado", la altura del árbol pasa a ser $n$ y la complejidad de las operaciones colapsa a un ineficiente **$O(n)$**. Esto justifica la existencia de variantes auto-balanceables como los árboles AVL o Rojo-Negro.
