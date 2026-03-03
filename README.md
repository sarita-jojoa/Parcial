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


<img width="801" height="503" alt="image" src="https://github.com/user-attachments/assets/31219550-120b-4257-acf3-91498a62e886" />
