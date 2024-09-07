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



### Desarrollo

1. **Tabla de Frecuencias de Ocurrencia de Caracteres:**
   El programa genera un diccionario, donde las claves son los caracteres que aparecen en el texto, y los valores, la cantidad de veces que este aparece en el texto. Para esto se lee caracter a caracter el texto y se van contando los caracteres.

2. **Simulación de una Fuente Discreta Sin Memoria:**
   Se toman los caracteres anteriores, y su cantidad de repeticiones para ponderarlos en la funcion random.choices(), luego la funcion retorna caracteres aleatorios, siendo los mas probables los mas repetidos. Para usarla, se usa la funcon generar_fuetne() a la cual se le envía el diccionario (o tabla) y devuelve una función que hace lo descrito anteriormente, basandose en la tabla enviada, con ademas la posibilidad de pedir mas de 1 caracter.
3. **Generación de un Codificador Huffman:**
   Para implementear el codificador Huffman se procedio como sigue:
      * Se generar primero un arbol binario, a partir de la tabla con frecuencias. Se implemento el algoritomo de Huffman, siendo este conocido, se explican solo detalles relativos a la implementacion:
         * Se forman tuplas de la forma (frecuencia, identificador, caracter(es)), de esta forma podemos realizar la comparacion de frecuencias, comparando tuplas. El identificador sirve para resolver las equivalencias en repeticiones, y finalmente el ultimo elemento puede ser un caracter o una tupla de caracters o tupla de tuplas de... . De esta forma, cada tupla de 3 elementos represanta un sub arbol. Los nodos estarían representado en cada tupla de 2 elementos, las que contienen caracteres o tuplas de. 
         * Se ordenan los elementos con heapify(), de forma que estan ordenados por frecuencia. Luego se toman los 2 ultimos, y se agrega un nuevo nodo que contiene a los quitados, este se introduce a través del metodo heappush()
         con el fin mantener el orden y poder repetir estos pasos para contruir el arbol. El nuevo "nodo" tiene :
            * frecuencia = f1 + f2
            * k = k1
            * caracteres = (caracter(es)1, caracter(es)2)
            -Notar que se indica caracter(es) cuando el elemento puede ser un caracter solo o una tupla.
         * Una vez completado el arbol, representado por la tupla de tupals del elemento de 3 del ultimo elemento que queda del heap (Notar que esta es la condicion con la termina el algoritmo). Se retorna el arbol (tupla)

4. **Aplicación con un Texto de Proyecto Gutenberg:**
   - Evaluar la eficiencia del codificador.
      El codigo obtenido es mas eficiente que utf-8.
      El codigo genera un longitud media de palabra proxima a la entropia, tanto para el texto original como secuencias aleatorias generadas con la fuente del apartado anterior.

### Evaluación del Codificador
   Se observa que la longitud media del codigo es proxima a la entropía de la fuente. Esto nos da indicio de que es un codificador optimo. Lmed < Hfuente +  1


### Resultados y discusion
   El codigo permite codificar y decodificar todos los caracteres del texto entregado.
   La implementación se ejecuta en un tiempo largo (5s para el texto dado).
   Se observa que el codigo no solo es mas eficiente que unicode, sino que la longitud media de palabra, es próxima a la entropía de la fuente


## Conclusiones 
   A partir de este trabajo se pudo observar de manera práctica algunos resultados o conceptos de teoría de la información. En particular como se puede encontrar una manera 


### Referencias

1. Gallager, R. G. (1968). *Information Theory and Reliable Communication*. John Wiley & Sons.
2. Proakis, J. G., & Salehi, M. (2008). *Digital Communications* (5th ed.). McGraw-Hill.  



