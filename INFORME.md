# CC76TF2018TSP
Travelling Salesman Problem

Índice
1. Introducción

Se trata del **Problema del vendedor viajero** o tambien conocido con las siglas TSP (Travelling Salesman Problem). Dicho problema  
consiste en el recorrido de un conjunto de ciudades alrededor del mapa, el cual tiene como punto de inicio cualquier ciudad. La manera 
en la cual debe recorrer dicho viajero tiene algunos requerimientos: debe pasar por todas las ciudades, solo una sola vez por ciudad y 
tener el minimo costo de recorrido (tiempo, costo de viaje, distancia, etc). Luego de dicho recorrido debe regresar al punto inicial. 

A travez del tiempo, se ha producido algunas soluciones: Karl Menger (Shortest Hamiltonian Path, 1930), J.B. Robinson (Hamiltonian game, 
1949), G. Dantzig, R. Fulkerson, y S. Johnson (Instancia de 49 ciudades y una introducción de cortes y branching, 1954), M. Held and 
R.M. Karp (Introducción de heuristicas, 1962) o el mas reciente Cook, Espinoza and Goycoolea (Instancia de 33 000 ciudades, 2005)

El presente trabajo realiza una invesigacion, dentro del marco del Trabajo Parcial para el curso de Complejidad Algoritmica, sobre dicho 
problema planteado. En primer lugar, se analizara los motivos y las implementaciones en la vida real de dicho problema. En segundo 
lugar, se analizara el problema, los requistos y el manejo de la data base. En tercer lugar, los objetivos a cumplir. En cuarto lugar se 
dara un repaso sobre los temas a utilizar. En quinto lugar,se mostrara la posible solucion para luego, en el sexto punto, mostrar los 
algoritmos implementados para dicha solucion. Por ultimo se analizara la complejidad de la solucion (Big O). Y por ultimo, de dara las 
conclusiones segun nuestros objetivos

2. Motivación

Una de las principales motivaciones por las cuales se hace el presente trabajo son algunas de las aplicaciones que se le pueden dar a 
nuestro problema, como son: Enrutamientos de vehiculos, estudio de la secuencia de genes, observacion astrologica, diseño de chips y 
otros problemas algoritmicos.

3. Problema

Dada una colección de ciudades y el costo de viaje entre cada par de ellas, el **TSP** se trata de encontrar el camino más barato en el 
que se visiten todas estas ciudades y regresar al punto inicial. En su versión estandar, el costro del viaje es simétrico en el sentido 
que viajar de la ciudad A hacia la ciudad B cuesta lo mismo que viajar de B hacia A.
La simplicidad del enunciado de este problema es engañosa, dado que el TSP es uno de los problemas en matemática computacional más 
intensamente estudiado y aún no se conoce una solución efectiva para todos los casos.
Aunque la compejidad del TSP aún es desconocida, por más de 50 años su estudio ha guiado el camino para métodos de solución mejorados en 
muchas áreas de optimización matemática.

4. Objetivos

  - Objetivo General
        - Mostrar el camino mas corto sobre la base de datos(puntos de coordenadas).
  - Objetivos Secundarios
        - Implementar el ingreso de la ciudad a la que se quiere llegar.
        - Experimentar el algoritmo con las 25 capitales regionales.
        - Experimentar el algoritmo con las 171 capitales provinciales.
        - Experimentar el algoritmo con las 1687 capitales distritales.
        - Experimentar el algoritmo con 143'351 centros poblados restantes.
        - Implementar tecnicas de programacion y algoritmos.

5. Marco Teórico 

  - Algoritmos Greeedy: 
    Tan bien llamado Algoritmo voraz cuyo proposito es encontrar una solucion optima. Para ello sigue un proceso secuencial en el que a
    cada paso toma una decisión (decide qué valor del dominio le ha de asignar a la variable actual) aplicando siempre el mismo criterio.
    La decisión es localmente óptima, es decir, ningún otro valor de los disponibles para esa variable lograría que la función objetivo
    tuviera un valor mejor, y luego comprueba si la puede incorporar a la secuencia de decisiones que ha tomado hasta el momento, es 
    decir, comprueba que la nueva decisión junto con todas las tomadas anteriormente no violan las restricciones y así consigue una 
    nueva secuencia de decisiones factible. 
    
   
    data_set2 - entre 1 a 2 segundos
    date_set3 - distritos entre 3 a 4 segundos
    
6. Solucion

    a. Prueba numero 1 .- Consiste en adjuntar los 25 capitales regionales (puntos de coordenadas) en un txt y probar el algoritmo.
      
    b. Prueba numero 2 .- Consiste en adjuntar los 171 capitales regionales (puntos de coordenadas) en un txt y probar el algoritmo.
      
    c. Prueba numero 3 .- Consiste en adjuntar los 1687 capitales regionales (puntos de coordenadas) en un txt y probar el algoritmo.
    
    
8. Algoritmo implementado

**Lectura de texto**
  ```python
def Read(filename):
    G = []
    i = 0
    file = open(filename)
    for line in file:
        G.append([float(x) for x in line.split('\t')])
  ```
**Calculo de distancia**
```python
def distancia(nodo1, nodo2):
    return ((nodo1[0] - nodo2[0])**2 + (nodo1[1] - nodo2[1])**2) ** 0.5

```

  a). 1er Algoritmo: **Algoritmo Greedy**

```python
def tsp(G, s=None):
    if s is None:
        s = G[0]
    por_visitar = G
    camino = [s]
    por_visitar.remove(s)
    while por_visitar:
        proximo = min(por_visitar, key=lambda x: distancia(camino[-1], x))
        camino.append(proximo)
        por_visitar.remove(proximo)
    return camino
G = Read('dataset.txt')
print(tsp(G))
G2 = Read('dataset2.txt')
print(tsp(G2))
G3 = Read('dataset3.txt')
print(tsp(G3))
G4 = Read('dataset4.txt')
print(tsp(G4))

```
  b)2do Algoritmo **Algoritmo prim**
- Creacion del Grafo de puntos de llegada - distancia

```python
    def Grafito(CPoblados):
    n = len(CPoblados)
    G = [[] for _ in range(n)]
    N = []
    for _ in range(n):
        N.append(_)
    j = -1
    for i in CPoblados:
        auxiliar = CPoblados[:]
        auxiliar.remove(i)
        CantDestNodo = rnd.randint(2,3)
        j +=1
        for _ in range(CantDestNodo):
            dest = rnd.choice(auxiliar)
            auxiliar.remove(dest)
            dist = distancia(i,dest)
            conexion = (dist, int(CPoblados.index(dest)))
            G[j].append(conexion)
    return G

```
  - Prim
   
``` python
import math
import heapq as hq

def prim(G):
    n = len(G)
    dist = [math.inf]*n
    path = [-1]*n
    visited = [False]*n
    q = []
    hq.heappush(q, (0, 0))
    dist[0] = 0
    while len(q) > 0:
        _, u = hq.heappop(q)
        if not visited[u]:
            visited[u] = True
            for w, v in G[u]:
                if not visited[v] and w < dist[v]:
                    dist[v] = w
                    path[v] = u
                    hq.heappush(q, (w, v))

    return path, dist

```
  - Dijkstra
   
``` python

def dijkstra(G, s):
    n = len(G)
    visited = [False]*n
    weights = [math.inf]*n
    path = [None]*n
    queue = []
    weights[s] = 0
    c = 0
    hq.heappush(queue, (0, s))
    while len(queue) > 0:
        g, u = hq.heappop(queue)
        visited[u] = True
        for w, v in G[u]:
            if not visited[v]:
                f = g + w
                if f < weights[v]:
                    weights[v] = f
                    path[v] = u
                    c += w
                    hq.heappush(queue, (f, v))
    return path, weights, c
    
    
    
```



9. Bibliografia

(1) ESPINOZA, Daniel. El Problema del Vendedor Viajero (TSP) y Programación Entera (IP).Chile. Universidad de Chile. [http://www.dii.uchile.cl/~daespino/PApers/TSP_and_IP_chile_050820.pdf](http://www.dii.uchile.cl/~daespino/PApers/TSP_and_IP_chile_050820.pdf) (Consultado el dia 13 de setiembre de 2018)

(2) COOK, William. The Travelling Salesman Problem. Canada. University of Waterloo. [http://www.math.uwaterloo.ca/tsp/problem/index.html]

(3) Traveling Salesman Problem (TSP) Implementation
[https://www.geeksforgeeks.org/traveling-salesman-problem-tsp-implementation/]

(4)Travelling salesman using brute-force and heuristics
[https://codereview.stackexchange.com/questions/81865/travelling-salesman-using-brute-force-and-heuristics]
