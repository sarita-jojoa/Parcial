# Parcial
```python
import random
import time

def merge_sort(lista):
    # Si la lista tiene más de un elemento, se puede dividir
    if len(lista) > 1:

        # 1. Dividir la lista en dos mitades
        mid = len(lista) // 2
        izquierda = lista[:mid]
        derecha = lista[mid:]

        # 2. Se ordenan recursivamente
        merge_sort(izquierda)
        merge_sort(derecha)

        # 3. Mezclar las mitades ordenadas
        i = j = k = 0

        # Comparar elementos de izquierda y derecha
        while i < len(izquierda) and j < len(derecha):
            if izquierda[i] < derecha[j]:
                lista[k] = izquierda[i]
                i += 1
            else:
                lista[k] = derecha[j]
                j += 1
            k += 1

        # Copiar los elementos restantes de la izquierda
        while i < len(izquierda):
            lista[k] = izquierda[i]
            i += 1
            k += 1

        # Copiar los elementos restantes de la derecha
        while j < len(derecha):
            lista[k] = derecha[j]
            j += 1
            k += 1


# Cantidad de datos
n = 100000

# Generar lista de números aleatorios
datos = [random.randint(1, 1_000_000) for _ in range(n)]

# Medir tiempo antes de ordenar
inicio = time.time()

# Ordenar usando Merge Sort (primer algoritmo)
merge_sort(datos)

# Medir tiempo después de ordenar
fin = time.time()

# Resultados
print("Cantidad de datos:", n)
print("Tiempo de ejecución:", fin - inicio, "segundos")

# Este sistema trabaja con grandes cantidades de datos, se ejecuta varias veces al día y debe 
# presentarse en el menor tiempo posible, esto nos lleva a elegir el algoritmo con (Merge Sort), 
# ya que su notación de complejidad O(n log n) garantiza un rendimiento efeciente y estable,
# independientemente del orden inicial de los datos, esto hace que se mantenga constante al 
# incrementar los datos sin tener que duplicar el tiempo mientras estos aumentan y sea más 
# rapido ante los demás algoritmos.
```
## salida de consola
<img width="827" height="147" alt="image" src="https://github.com/user-attachments/assets/1dfb86c5-7298-4ee5-9957-6e302559acc6" />

## medición de rendimiento de todos los algoritmos
```python
import random
import time

# Generar 10.000 datos aleatorios
n = 10000
datos = [random.randint(0, 1000000) for _ in range(n)]

# Copias para cada algoritmo
bubble_lista = datos.copy()
insertion_lista = datos.copy()
selection_lista = datos.copy()
merge_lista = datos.copy()
quick_lista = datos.copy()

# ---------------- BUBBLE SORT ----------------
def bubble_sort(lista):
    for i in range(len(lista)):
        for j in range(0, len(lista)-i-1):
            if lista[j] > lista[j+1]:
                lista[j], lista[j+1] = lista[j+1], lista[j]

# ---------------- INSERTION SORT ----------------
def insertion_sort(lista):
    for i in range(1, len(lista)):
        clave = lista[i]
        j = i - 1
        while j >= 0 and clave < lista[j]:
            lista[j + 1] = lista[j]
            j -= 1
        lista[j + 1] = clave

# ---------------- SELECTION SORT ----------------
def selection_sort(lista):
    for i in range(len(lista)):
        min_idx = i
        for j in range(i+1, len(lista)):
            if lista[j] < lista[min_idx]:
                min_idx = j
        lista[i], lista[min_idx] = lista[min_idx], lista[i]

# ---------------- MERGE SORT ----------------
def merge_sort(lista):
    if len(lista) > 1:
        mid = len(lista)//2
        izquierda = lista[:mid]
        derecha = lista[mid:]

        merge_sort(izquierda)
        merge_sort(derecha)

        i = j = k = 0
        while i < len(izquierda) and j < len(derecha):
            if izquierda[i] < derecha[j]:
                lista[k] = izquierda[i]
                i += 1
            else:
                lista[k] = derecha[j]
                j += 1
            k += 1

        while i < len(izquierda):
            lista[k] = izquierda[i]
            i += 1
            k += 1

        while j < len(derecha):
            lista[k] = derecha[j]
            j += 1
            k += 1

# ---------------- QUICK SORT ----------------
def quick_sort(lista):
    if len(lista) <= 1:
        return lista
    pivote = lista[len(lista)//2]
    izquierda = [x for x in lista if x < pivote]
    centro = [x for x in lista if x == pivote]
    derecha = [x for x in lista if x > pivote]
    return quick_sort(izquierda) + centro + quick_sort(derecha)

# ---------------- MEDICIÓN ----------------
def medir_tiempo(funcion, lista):
    inicio = time.time()
    funcion(lista)
    fin = time.time()
    return fin - inicio

print("Merge Sort:", medir_tiempo(merge_sort, merge_lista))
print("Quick Sort:", medir_tiempo(lambda x: quick_sort(x), quick_lista))
print("Bubble Sort:", medir_tiempo(bubble_sort, bubble_lista))
print("Insertion Sort:", medir_tiempo(insertion_sort, insertion_lista))
print("Selection Sort:", medir_tiempo(selection_sort, selection_lista))

```
## salida de consola
<img width="366" height="177" alt="image" src="https://github.com/user-attachments/assets/04c34293-02f8-43f3-a33a-ee8896f56956" />
## concluciones 
podemos darnos cuenta que los más rapidos son merge sort y quick sort por lo cúal son los mas convenientes, en este caso no elegimos quick porque en su peor caso puede caer en notación big (n²) el cual cuadruplicaria el tiempo mientras aumentan los datos, aunque es el más rapido debemos prevenir que cuadruplique el tiempo entonces elegimos merge sort, ya que se mantiene constante con sus resultados a pesar de que los datos aumenten sin presentar cambios en el tiempo.

<img width="801" height="503" alt="image" src="https://github.com/user-attachments/assets/31219550-120b-4257-acf3-91498a62e886" />


## Bubble Sort

-Mejor caso: O(n)

Cuando la lista ya está ordenada y el algoritmo está optimizado con una bandera de verificación, solo necesita una pasada para comprobar que no hay intercambios.
No realiza cambios, solo comparaciones lineales.

-Caso promedio: O(n²)

En datos desordenados, cada elemento debe compararse muchas veces con los demás.
Se usan dos ciclos anidados que recorren casi toda la lista.

-Peor caso: O(n²)

Si la lista está en orden inverso, realiza el máximo número de comparaciones e intercambios posibles.

## Insertion Sort

-Mejor caso: O(n)

Si la lista ya está ordenada, cada elemento solo se compara una vez con el anterior y no necesita desplazarse.

-Caso promedio: O(n²)

Cada elemento puede necesitar moverse varias posiciones hacia la izquierda para quedar en su lugar correcto.

-Peor caso: O(n²)

Si está en orden inverso, cada nuevo elemento debe desplazarse hasta el inicio del arreglo, generando muchas comparaciones y movimientos.

## Selection Sort

-Mejor caso: O(n²)

Siempre recorre toda la parte no ordenada para encontrar el mínimo, incluso si la lista ya está ordenada.

-Caso promedio: O(n²)

El número de comparaciones es siempre el mismo porque busca el mínimo en cada iteración.

-Peor caso: O(n²)

Independientemente del orden inicial, realiza la misma cantidad de comparaciones.

## Merge Sort

-Mejor caso: O(n log n)

Divide la lista en mitades sucesivamente (log n divisiones) y luego combina recorriendo todos los elementos (n).

-Caso promedio: O(n log n)

El proceso de dividir y mezclar es el mismo sin importar el orden inicial.

-Peor caso: O(n log n)

Siempre realiza las mismas divisiones y combinaciones, por eso su tiempo es estable.

## Quick Sort

-Mejor caso: O(n log n)

Cuando el pivote divide la lista en dos partes casi iguales, se logran log n niveles de división y n comparaciones por nivel.

-Caso promedio: O(n log n)

Generalmente el pivote divide la lista de forma equilibrada, manteniendo buena eficiencia.

-Peor caso: O(n²)

Si el pivote divide muy mal (por ejemplo, lista ya ordenada y pivote mal elegido), se generan divisiones muy desbalanceadas y se comporta como un algoritmo cuadrático.

