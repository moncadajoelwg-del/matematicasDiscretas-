# TEORÍA DE GRAFOS 

## 1. Anatomía y Representación de un Grafo
Un **grafo conecta vértices (nodos) mediante aristas (arcos)** para modelar redes y relaciones.

* **Grado:** Número de conexiones de un vértice.
* **Direccionalidad:** Puede ser no dirigido (bidireccional) o dirigido (unidireccional).
* **Diagramas:** Representación geométrica tradicional mediante nodos y líneas.
* **Matriz de Adyacencia:** Cuadrícula matemática binaria (1 y 0). Ideal para grafos densos.
* **Lista de Adyacencia:** Lista compacta de vecinos directos. Eficiente en memoria para grafos dispersos.

---

## 2. Caminos vs. Circuitos

* **Paseo (Walk):** Movimiento libre. Permite repetir vértices y aristas.
* **Camino (Path):** Recorrido con restricciones. Todos los vértices y aristas deben ser distintos.
* **Circuito (Cycle):** Viaje redondo. Es un camino que empieza y termina en el mismo vértice.

### Cuadro Comparativo

| Tipo de Recorrido | ¿Repite Vértices? | ¿Repite Aristas? | ¿Inicio y Fin iguales? |
| :--- | :--- | :--- | :--- |
| **Paseo** | Sí | Sí | No necesariamente |
| **Camino** | No | No | No |
| **Circuito** | No (solo origen/fin) | No | **Sí** |

---

## 3. Exploración por Aristas: Enfoque de Euler
El objetivo es recorrer cada arista **exactamente una vez**. Requiere un grafo conexo.

* **Paseo de Euler:** Pasa por todas las aristas y termina en un vértice diferente al de inicio. Existe si y solo si hay **exactamente dos vértices con grado impar**.
* **Circuito de Euler:** Pasa por todas las aristas y regresa al origen. Existe si y solo si **todos sus vértices tienen grado par**.

---

## 4. Exploración por Nodos: Enfoque de Hamilton
El objetivo es visitar cada vértice **exactamente una vez**, ignorando si quedan aristas libres.

* **Paseo de Hamilton:** Visita todos los nodos una vez. El punto final es distinto al inicial.
* **Circuito de Hamilton:** Visita todos los nodos una vez y regresa limpiamente al origen. Es un problema NP-completo (sin teorema definitivo de existencia).
* **Teorema de Dirac:** Garantiza circuito si cada nodo tiene un grado $\ge n/2$ (donde $n \ge 3$ es el número de vértices).
* **Teorema de Ore:** Garantiza circuito si la suma de grados de cualquier par de vértices no adyacentes es $\ge n$.

---

## 5. Análisis y Optimización de Algoritmos
La optimización evita la fuerza bruta y reduce la complejidad temporal de exponencial $O(2^n)$ a polinomial $O(n^2)$, ahorrando memoria y CPU.

* **Algoritmo de Fleury (Euler):** Construye rutas eulerianas con la regla de **no cruzar una arista de corte (puente)** a menos que sea la única opción. Complejidad clásica: $O(|E|^2)$, donde $|E|$ es el número de aristas.
* **Algoritmo de Dijkstra (Camino corto):** *(Texto interrumpido en el original)*. Diseñado para hallar la ruta de menor costo o distancia desde un nodo origen hacia los demás.
