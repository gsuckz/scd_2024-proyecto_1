# Codificador de fuente para una fuente discreta sin memoria
#### Jesus Gerardo Daniel Avila


## Introduccion

1. **Fuente de Información Discreta y Fuente Discreta Sin Memoria (DMS):**
   - Una **fuente de información discreta** es un modelo matemático que emite una secuencia de símbolos de un alfabeto finito con ciertas probabilidades. Cada símbolo puede tener una probabilidad distinta de aparecer.
   - Una **fuente discreta sin memoria (DMS)** es un tipo específico de fuente de información discreta en la cual la emisión de un símbolo es independiente de las emisiones anteriores. Es decir, las probabilidades de los símbolos no dependen del contexto.

2. **Entropía y Entropía de una DMS:**
   - La **entropía** es una medida de la incertidumbre o aleatoriedad en la salida de una fuente de información. Se define como el promedio ponderado del logaritmo del inverso de las probabilidades de los símbolos emitidos por la fuente.

3. **Codificación de Fuente:**
   - La **codificación de fuente** se refiere a la transformación de los símbolos de una fuente de información en una secuencia de bits.
    El objetivo es reducir la redundancia en la secuencia de salida. O reducir la cantidad de bits enviados.
   - **Unicode** es un estándar de codificación de caracteres que permite representar la mayoría de los sistemas de escritura del mundo. **UTF-8** es una forma de codificación de Unicode que usa de 1 a 4 bytes para representar cada carácter, lo que la hace eficiente y compatible con ASCII.

4. **Codificación Óptima para una DMS y Teorema de Codificación de Fuente:**
   - Una **codificación óptima** para una DMS minimiza la longitud media del código. El **teorema de codificación de fuente** establece que es posible codificar los símbolos de una fuente de manera que la longitud media del código se acerque a la entropía de la fuente.
   - **Codificación Huffman** es un algoritmo que genera un código binario de longitud mínima para un conjunto dado de símbolos con probabilidades conocidas, siendo óptimo para fuentes discretas sin memoria.

5. **Ley de los Grandes Números:**
   - Esta ley afirma que, dado un número suficientemente grande de repeticiones de un experimento aleatorio, la frecuencia relativa de un evento tiende a converger hacia su probabilidad teórica.
   - Se aplica en la estimación de probabilidades de los símbolos de una DMS basada en una muestra de su salida, permitiendo aproximar las probabilidades reales a partir de la observación de la secuencia de salida.


### Referencias

1. Gallager, R. G. (1968). *Information Theory and Reliable Communication*. John Wiley & Sons.
2. Proakis, J. G., & Salehi, M. (2008). *Digital Communications* (5th ed.). McGraw-Hill.  

### Implementación en Python

1. **Tabla de Frecuencias de Ocurrencia de Caracteres:**
   ```python
   def calcular_frecuencias(archivo):
       frecuencias = {}
       with open(archivo, 'r', encoding='utf-8') as f:
           for linea in f:
               for caracter in linea:
                   if caracter in frecuencias:
                       frecuencias[caracter] += 1
                   else:
                       frecuencias[caracter] = 1
       return frecuencias
   ```

2. **Simulación de una Fuente Discreta Sin Memoria:**
   ```python
   import random

   class FuenteDMS:
       def __init__(self, simbolos, probabilidades):
           self.simbolos = simbolos
           self.probabilidades = probabilidades

       def generar_cadena(self, longitud):
           return ''.join(random.choices(self.simbolos, self.probabilidades, k=longitud))
   ```

3. **Generación de un Codificador Huffman:**
   ```python
   from heapq import heappush, heappop, heapify

   def codificador_huffman(tabla_prob):
       heap = [[peso, [simbolo, ""]] for simbolo, peso in tabla_prob.items()]
       heapify(heap)
       while len(heap) > 1:
           lo = heappop(heap)
           hi = heappop(heap)
           for par in lo[1:]:
               par[1] = '0' + par[1]
           for par in hi[1:]:
               par[1] = '1' + par[1]
           heappush(heap, [lo[0] + hi[0]] + lo[1:] + hi[1:])
       return sorted(heappop(heap)[1:], key=lambda p: (len(p[-1]), p))

   ```

4. **Aplicación con un Texto de Proyecto Gutenberg:**
   - Obtener un libro en texto plano en UTF-8.
   - Calcular las frecuencias de los caracteres.
   - Crear una simulación de la fuente DMS y el codificador Huffman.
   - Evaluar la eficiencia del codificador.

### Evaluación del Codificador
Para verificar si el codificador Huffman cumple con el Teorema de Codificación de Fuente, compara la longitud promedio del código generado con la entropía de la fuente. Si la longitud media se aproxima a la entropía, el codificador es eficiente.

Este proyecto aborda los conceptos teóricos y su implementación práctica, lo que permite una comprensión profunda y la aplicación de estos conceptos en la vida real.









