# TEORÍA DE GRAFOS 

## 1. Anatomía y Representación de un Grafo
Un **grafo conecta vértices (nodos) mediante aristas (arcos)** para modelar redes y relaciones.

* **Grado:** Número de conexiones de un vértice.
* **Direccionalidad:** Puede ser no dirigido (bidireccional) o dirigido (unidireccional).
* **Diagramas:** Representación geométrica tradicional mediante nodos y líneas.
* **Matriz de Adyacencia:** Cuadrícula matemática binaria (1 y 0). Ideal para grafos densos.
* **Lista de Adyacencia:** Lista compacta de vecinos directos. Eficiente en memoria para grafos dispersos.

---

### a. Diaggrama de Nodos y Enlaces (Grafo No Dirigido)
Representación geométrica tradicional. El **Nodo B** actúa como el puente principal (influencer) con el mayor **grado** de la red.

```mermaid
graph LR
    A((Nodo A)) --- B((Nodo B))
    B((Nodo B)) --- C((Nodo C))
    B((Nodo B)) --- D((Nodo D))
    
    style B fill:#f9f,stroke:#333,stroke-width:4px
```

---

### b. Direccionalidad (Grafo Dirigido / Unidireccional)
Representación donde las relaciones tienen un sentido único (flechas).

```mermaid
graph TD
    A((Nodo A)) --> B((Nodo B))
    B((Nodo B)) --> C((Nodo C))
    C((Nodo C)) --> A((Nodo A))
    B((Nodo B)) --> D((Nodo D))
```

---

### c. Matriz de Adyacencia (Representación Estructural)
Cuadrícula matemática binaria. El siguiente diagrama mapea de forma visual cómo se estructuran los `1` (conexión) y `0` (sin conexión) en la memoria.
```mermaid
quadrantChart
    title Matriz Binaria de Conexiones
    x-axis "Sin Conexión (0)" --> "Conectado (1)"
    y-axis "Filas (Nodos Origen)" --> "Columnas (Nodos Destino)"
    quadrant-1 "Alta Densidad: Muchos 1s"
    quadrant-2 "Grafo Dirigido Asimétrico"
    quadrant-3 "Baja Densidad: Muchos 0s"
    quadrant-4 "Grafo No Dirigido Simétrico"
```
---

### d. Lista de Adyacencia (Estructura Compacta)
Formato de lista ideal para ahorrar memoria en grafos dispersos, mostrando únicamente los vecinos directos.

```mermaid
graph LR
    subgraph Lista de Adyacencia
        N0[Nodo A] --> V0[Vecino: B]
        N1[Nodo B] --> V1[Vecino: A] & V2[Vecino: C] & V3[Vecino: D]
        N2[Nodo C] --> V4[Vecino: B]
        N3[Nodo D] --> V5[Vecino: B]
    end
    
    style N0 fill:#fff,stroke:#333
    style N1 fill:#fff,stroke:#333
    style N2 fill:#fff,stroke:#333
    style N3 fill:#fff,stroke:#333
```
---


## 2. Caminos vs. Circuitos (Visualización de Rutas)

Para los siguientes ejemplos, utilizaremos un grafo de 4 nodos conectados en anillo con una diagonal interna. Las líneas gruesas y de colores representan el recorrido realizado.

### A. Paseo (Walk)
*   **Regla:** Movimiento libre. Permite repetir nodos y líneas.
*   **Ejemplo de Ruta:** `A -> B -> C -> B -> A`. (Repite el nodo **B** y las aristas entre ellos).

```mermaid
graph LR
    A((A)) === B((B))
    B === C((C))
    C --- D((D))
    D --- A
    A --- C

    linkStyle 0,1 stroke:#ffc107,stroke-width:4px;
```

---

### B. Camino (Path)
*   **Regla:** Recorrido con restricciones estrictas. Todos los vértices y aristas deben ser únicos.
*   **Ejemplo de Ruta:** `A -> B -> C -> D`. (No repite absolutamente nada).

```mermaid
graph LR
    A((A)) === B((B))
    B === C((C))
    C === D((D))
    D --- A
    A --- C

    linkStyle 0,1,2 stroke:#28a745,stroke-width:4px;
```

---

### C. Circuito (Cycle)
*   **Regla:** Viaje redondo. Es un camino cerrado que empieza y termina en el mismo nodo, sin repetir elementos intermedios.
*   **Ejemplo de Ruta:** `A -> B -> C -> A`. (Regresa limpiamente al origen).

```mermaid
graph LR
    A((A)) === B((B))
    B === C((C))
    C --- D((D))
    D --- A
    A === C

    linkStyle 0,1,4 stroke:#007bff,stroke-width:4px;
```

---

### D. Árbol de Decisión Comercial: ¿Qué recorrido necesitas?
Diagrama interactivo para clasificar el tipo de movimiento en la red según tus restricciones.

```mermaid
graph TD
    Start([¿El punto de inicio y fin es el mismo?]) -->|Sí| CheckRep1["¿Se repiten nodos intermedios?"]
    Start -->|No| CheckRep2["¿Se repiten nodos o aristas?"]

    CheckRep1 -->|Sí| PaseoCerrado["Paseo Cerrado"]
    CheckRep1 -->|No| Circuito["Circuito / Ciclo (Cycle)"]

    CheckRep2 -->|Sí| Paseo["Paseo (Walk)"]
    CheckRep2 -->|No| Camino["Camino (Path)"]

    style Circuito fill:#d4edda,stroke:#28a745,stroke-width:2px
    style Camino fill:#d4edda,stroke:#28a745,stroke-width:2px
    style Paseo fill:#fff3cd,stroke:#ffc107,stroke-width:2px
    style PaseoCerrado fill:#fff3cd,stroke:#ffc107,stroke-width:2px
```
---

## 3. Exploración por Aristas: Enfoque de Euler

### A. Paseo de Euler (Camino Euleriano)
*   **Regla:** Pasa por todas las aristas una vez y termina en un nodo diferente al de inicio.
*   **Condición:** Exactamente **dos vértices impares** (los nodos **A** y **D** tienen grado 3). El recorrido válido es: `A -> B -> C -> D -> B -> A -> D`.

```mermaid
graph LR
    A((A: Grado 3)) --- B((B: Grado 4))
    A --- D((D: Grado 3))
    B --- C((C: Grado 2))
    B --- D
    C --- D
    B --- A

    style A fill:#ff9999,stroke:#333,stroke-width:2px
    style D fill:#ff9999,stroke:#333,stroke-width:2px
```

---

### B. Circuito de Euler (Ciclo Euleriano)
*   **Regla:** Pasa por todas las aristas una vez y regresa exactamente al nodo de origen.
*   **Condición:** **Todos los vértices son pares** (todos tienen grado 2 o 4). Un recorrido válido empezando en A es: `A -> B -> C -> D -> B -> A`.

```mermaid
graph LR
    A((A: Grado 2)) --- B((B: Grado 4))
    B --- C((C: Grado 2))
    C --- D((D: Grado 2))
    D --- B
    B --- A

    style B fill:#99ff99,stroke:#333,stroke-width:2px
```

---

### C. Criterio de Decisión de Euler
Diagrama de flujo interactivo para saber rápidamente qué tipo de recorrido euleriano posee un grafo según el grado de sus nodos.

```mermaid
graph TD
    Start([¿El grafo es conexo?]) -->|No| NoEuler["No es Euleriano"]
    Start -->|Sí| Count[Contar vértices con grado impar]
    
    Count -->|Tiene 0 impares| Circuito["Circuito de Euler (Todos pares)"]
    Count -->|Tiene 2 impares| Paseo["Paseo de Euler (Inicio != Fin)"]
    Count -->|Cualquier otra cantidad| NoPosible["No tiene ruta de Euler"]

    style Circuito fill:#d4edda,stroke:#28a745,stroke-width:2px
    style Paseo fill:#fff3cd,stroke:#ffc107,stroke-width:2px
    style NoPosible fill:#f8d7da,stroke:#dc3545,stroke-width:2px
```
---
## 4. Exploración por Nodos: Enfoque de Hamilton
El objetivo es visitar cada vértice **exactamente una vez**, ignorando si quedan aristas libres.

* **Paseo de Hamilton:** Visita todos los nodos una vez. El punto final es distinto al inicial.
* **Circuito de Hamilton:** Visita todos los nodos una vez y regresa limpiamente al origen. Es un problema NP-completo (sin teorema definitivo de existencia).
* **Teorema de Dirac:** Garantiza circuito si cada nodo tiene un grado $\ge n/2$ (donde $n \ge 3$ es el número de vértices).
* **Teorema de Ore:** Garantiza circuito si la suma de grados de cualquier par de vértices no adyacentes es $\ge n$.

### A. Paseo de Hamilton (Camino Hamiltoniano)
*   **Regla:** Visita todos los vértices exactamente una vez. Pueden quedar aristas sin usar y el inicio es diferente al fin.
*   **Ejemplo de Ruta:** `A -> B -> C -> D`. (Todos los nodos tocados una sola vez).

```mermaid
graph LR
    A((A)) === B((B))
    B === C((C))
    C === D((D))
    D --- A
    B --- D

    linkStyle 0,1,2 stroke:#28a745,stroke-width:4px;
```

---

### B. Circuito de Hamilton (Ciclo Hamiltoniano)
*   **Regla:** Visita todos los vértices exactamente una vez y regresa limpiamente al origen.
*   **Ejemplo de Ruta:** `A -> B -> C -> D -> A`. (Viaje redondo perfecto por todos los nodos).

```mermaid
graph LR
    A((A)) === B((B))
    B === C((C))
    C === D((D))
    D === A
    B --- D

    linkStyle 0,1,2,3 stroke:#007bff,stroke-width:4px;
```

---

### C. Teoremas de Suficiencia (Dirac y Ore)
Mapa conceptual interactivo para verificar si un grafo denso tiene garantizado un Circuito de Hamilton según las condiciones analíticas de sus grados.

```mermaid
graph TD
    Start([¿El grafo tiene n >= 3 vertices?]) -->|No| NoAplica["No aplican estos teoremas"]
    Start -->|Sí| Analisis{"¿Que propiedad vas a evaluar?"}
    
    Analisis -->|Grado individual de cada nodo| Dirac["Teorema de Dirac"]
    Analisis -->|Suma de nodos no conectados| Ore["Teorema de Ore"]

    Dirac --> CondDirac{"¿Cada nodo tiene grado >= n/2?"}
    CondDirac -->|Sí| SeguroDirac["Circuito Hamiltoniano Garantizado"]
    CondDirac -->|No| Inconcluyente1["Inconcluyente (Podria tenerlo o no)"]

    Ore --> CondOre{"¿Suma de grados de pares no adyacentes >= n?"}
    CondOre -->|Sí| SeguroOre["Circuito Hamiltoniano Garantizado"]
    CondOre -->|No| Inconcluyente2["Inconcluyente (Podria tenerlo o no)"]

    style SeguroDirac fill:#d4edda,stroke:#28a745,stroke-width:2px
    style SeguroOre fill:#d4edda,stroke:#28a745,stroke-width:2px
    style Inconcluyente1 fill:#e2e3e5,stroke:#6c757d,stroke-width:2px
    style Inconcluyente2 fill:#e2e3e5,stroke:#6c757d,stroke-width:2px
```


---

## 5. Análisis y Optimización de Algoritmos
La optimización evita la fuerza bruta y reduce la complejidad temporal de exponencial $O(2^n)$ a polinomial $O(n^2)$, ahorrando memoria y CPU.

* **Algoritmo de Fleury (Euler):** Construye rutas eulerianas con la regla de **no cruzar una arista de corte (puente)** a menos que sea la única opción. Complejidad clásica: $O(|E|^2)$, donde $|E|$ es el número de aristas.
* **Algoritmo de Dijkstra (Camino corto):** *(Texto interrumpido en el original)*. Diseñado para hallar la ruta de menor costo o distancia desde un nodo origen hacia los demás.

### A. Algoritmo de Fleury (Evitando Aristas de Corte / Puentes)
*   **Concepto:** La arista que une **B** y **C** es un puente (arista de corte). Si la cruzas muy pronto, aíslas el resto del grafo y la ruta falla. Fleury obliga a consumir primero los ciclos locales antes de cruzarla.

```mermaid
graph LR
    subgraph Componente Local 1
        A((A)) --- B((B))
        B --- D((D))
        D --- A
    end

    B ---|Arista de Corte / Puente| C((C))

    subgraph Componente Local 2
        C --- E((E))
        E --- F((F))
        F --- C
    end

    style B fill:#fff,stroke:#333
    style C fill:#fff,stroke:#333
    linkStyle 2 stroke:#dc3545,stroke-width:3px,stroke-dasharray: 5 5;
```

---

### B. Algoritmo de Dijkstra (Camino Más Corto)
*   **Concepto:** Encuentra la ruta con menor peso acumulado desde un origen (Nodo A). Las etiquetas en las flechas representan el costo o distancia entre los nodos.

```mermaid
graph LR
    A((A: Origen)) -->|Costo: 4| B((B))
    A -->|Costo: 2| C((C))
    B -->|Costo: 5| D((D))
    C -->|Costo: 1| B
    C -->|Costo: 8| D
    B -->|Costo: 2| D

    style A fill:#007bff,stroke:#fff,stroke-width:2px,color:#fff
    style D fill:#28a745,stroke:#fff,stroke-width:2px,color:#fff
```

---

### C. Flujo de Operación del Algoritmo de Dijkstra
Diagrama secuencial que muestra cómo procesa la optimización el algoritmo paso a paso en la memoria del computador.

```mermaid
graph TD
    Start([Inicio: Nodo Origen]) --> Init["Inicializar distancias: Origen = 0, los demas = Infinito"]
    Init --> Queue["Agregar todos los nodos a una Cola de Prioridad"]
    
    Queue --> Loop{"¿La cola esta vacia?"}
    Loop -->|No| Extract["Extraer el nodo 'U' con la menor distancia actual"]
    Loop -->|Sí| End([Fin: Rutas optimas encontradas])
    
    Extract --> Neighbors{"¿Tiene vecinos no visitados?"}
    Neighbors -->|Sí| Relax["Evaluar vecino 'V': Alt = Distancia(U) + Peso(U, V)"]
    Neighbors -->|No| Loop
    
    Relax --> Condition{"¿Alt < Distancia(V) actual?"}
    Condition -->|Sí| Update["Actualizar Distancia(V) = Alt y reordenar cola"]
    Condition -->|No| Neighbors
    Update --> Neighbors
```
---
---

## 🛠️ Portafolio de Evidencias: Aplicación Práctica de Grafos

Este apartado consolida el registro de las actividades prácticas, experimentales y autónomas desarrolladas durante el periodo académico en la asignatura de Matemáticas Discretas, evidenciando el dominio de la teoría de redes.

### 🗣️ 1. Componente ACD (Aprendizaje en Contacto con el Docente)
Actividades de sustentación, defensa oral de algoritmos y talleres evaluados directamente por el docente en el aula de clase.

### **[[Ver Anexo de Evidencias ACD (Google Drive)](https://drive.google.com/drive/folders/1aealLI-3X5CfW4aXvX3w6P1LhF1_UCdP?usp=drive_link)]**
---

### 🧪 2. Componente APE (Aprendizaje Práctico-Experimental)
Resolución de problemas de aplicación práctica y experimentación guiada para afianzar los conceptos de la unidad.
### **[[Ver Anexo de Evidencias APE (Google Drive)](https://drive.google.com/file/d/1PFhss0oNnzJ-ke0ivNAFkKTM8WBmW_fl/view?usp=drive_link)]**

---

### 📝 3. Componente AA (Aprendizaje Autónomo)
Trabajos de investigación individual y resolución de bancos de problemas desarrollados de forma independiente.

### **[[Ver Anexo de Evidencias AA (Google Drive)](https://drive.google.com/drive/folders/1CmSQdFvxGMDTbyjSQ9BxKOvArl7nofpB?usp=drive_link)]**
