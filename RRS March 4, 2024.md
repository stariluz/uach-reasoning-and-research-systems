# Unit 3: Informed Search
Not all the searches are "blind" in some cases, there exists any information that helps to guide the search by an specific way. Then:
> An informed search is not an exhaustive search, it is not exploring all the state space of the problem

And for that reason, there are faster and more efficient techniques in terms of memory requirements.

>The informed search thecniques are optimun in the choose of the next state to visit.

For an informed thecnique, the desition of who is the next state to visite is:

> The next state is the best state in the list "Opened".

Otherwise, the GST still looks the same:
```py
opened=[begin:getBegin(begin)]
closed=[]
ready=false
while ready==false:
    current=getNext(opened)
    if curret==goal:
        ready=true
        add(current, closed)
    else:
        expand(current, opened, closed)
```
Though, they not work as the blind searches. There are three diferences:
1. Now a state in the lists looks this:
    ```py
        father(state)
    state:f(state)
    ```

    Where:
    - `state` is the state we are talking about
    - `father(state)` is the father state of `state` in the search
    - `f(state)` is the utility value in the search for `state`

2. The operation `getNext()` now gets the best state from `opened`:
    ```py
        next=argmax{f(q)} # para q en Abiertos
    ```
    This means: the next state to visit is that one on `opened` that maximices the utility value. 

    >This is the reasion why the techniques of informed search are techniques of optimus search.

3. And the operation `expand()` changes a little too. Now for expand the current state we follow this rule:
    > Add all the sons of the current state to `opened`, except those that are already in `closed`, and if it is in `opened` we can replace the before saved when the new `f(state)` is better.



# Unidad 3. Búsqueda informada
No todas las búsquedas están "ciegas", en muchos casos algo se tiene de información" como para guiar la búsqueda por un camino específico. Así que una búsqueda informada:

> Una búsqueda informada no es una búsqueda exhaustiva, no busca explorar todo el espacio estado del problema.

Y por esa razón suelen se técnicas mucho más rápidas y óptimas en lo que a sus requerimientos de memoria se refiere. Y no solo eso:

> Las técnicas de búsqueda informada son óptimas en cuanto a quien eligen como el siguiente estado a visitar.

Y es que para una técnica informada la decisión de quién es el siguiente estado a visitar es simple:

> El siguiente estado es el mejor estado en la lista Abiertos.

Osea que el AGB se sigue viendo igual:
```py
opened=[begin:getBegin(begin)]
closed=[]
ready=false
while ready==false:
    current=getNext(opened)
    if curret==goal:
        ready=true
        add(current, closed)
    else:
        expand(current, opened, closed)
```

Sin embargo no es igual a como funciona en las búsquedas ciegas. Existen 3 diferencias:
1. Ahora un estado en las listas y en general luce así:
    ```py
        father(state)
    state:f(state)
    ```

    Donde:
    - `state` es el estado en cuestion
    - `father(state)` es el estado padre de `state` en la búsqueda
    - `f(state)` es el valor de utilidad del estado `state`

2. La operación `getNext()`ahora extrae de abiertos al mejor estado en ella:
    ```py
        next=argmax{f(q)} # para q en Abiertos
    ```
    Es decir que el siguiente estado a visitar es aquel en Abiertos que maximice el valor de utilidad

    > Por esta razón las técnicas de búsqueda informada son técnicas de busqueda óptima

3. Y la operacion `expand()` también cambia un poco. Ahora para expandir al estado actual seguimos esta regla:
    >Agregar a todos los hijos del estado actual en Abiertos, excepto aquellos en Cerrados, y si está en Abiertos podemos reemplazar si este es mejor.
    
    De manera que ahora se puede reemplazar un estado en Abiertos, por una nueva versión de el mismo, si la nueva versión es "mejor" de acuerdo con su valor de utilidad.

## La utilidad de un estado
Ya conocemos que en una búsqueda informada un estado tiene un valor de utilidad al que denotamos como:
```py
f(state) # es la utilidad del estado
```
De este valor se tiene que `f(state) en R` y es esta utilidad lo que se llama "información" en una técnica de búsqueda informada. Sin embargo, no toda la información es igual. Es decir que:
> Aquello que `f(state)` describe tres técnicas de búsqueda informada
1. Primero por lo mejor
2. Búsqueda heuristica
3. Busqueda A estrella (A*)

La técnica **primero por lo mejor** considera que un estado se debe evaluar con su costo 
```py
f(state)=g(state)
```
siendo `g(state)` la función de costo de `state`.

La técnica de **búsqueda heuristica** considera que un estado se debe evaluar con algún valor heuristico
```py
f(state)=h(state)
```
siendo `h(state)` una función de valor heurístico.

La <strong>búsqueda A*</strong> dice que un estado se debe evaluar con ambos, su costo y su valor heurístico:

```py
f(state)=g(state)+h(state)
```
## El costo de un estado
Supongase que durante el proceso de búsqueda partiendo de $q_0$ se ha llegado a un estado $q_3$ siguiendo el camino $q_0 \to q_1 \to q_2 \to q_3$.

Entonces, según este camino $q_3$ tiene un costo $g(q_3) \in R_1$ y este coste se calcula de acuerdo a la siguiente regla:

$g(q_k)=\begin{Bmatrix} 
  0 \textrm{ si } q_k \textrm{ es el estado de inicio } \\
  g(q_{k-j})+C_{k-1,k}\textrm{ si } q_k \textrm{ no es el inicio }
\end{Bmatrix}$

Aquí $C_{k-1,k} \in \R$