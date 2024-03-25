# Course Checkpoint 4. Preguntas teóricas




## 1. Diferencia entre una lista y una tupla:
R. Las listas y tuplas son dos tipos de secuencias en Python, pero tienen diferencias clave:
- En el caso de las listas:
Son mutables, lo que significa que se puede modificar sus elementos después de crearlas.
Se definen usando corchetes [ ].
Se puede agregar, eliminar o cambiar elementos en una lista. Por ejemplo:

mi_lista = [1, 2, 3]
mi_lista.append(4)

- En el caso de las tuplas:

Son inmutables, lo que significa que no se puede modificar sus elementos una vez creadas.
Se definen usando paréntesis ( ).
Son más eficientes en términos de memoria y rendimiento. Además, cuando se usa Python para machine learning, muchas veces se debe decidir si se quiere tener mayor control sobre las estructuras de datos, así que cuando se trata de elegir entre una tupla y una lista, uno debe preguntarse si se trata de una estructura de datos que tengo que cambiar o es algo que quiero mantener. En otras palabras, si quiero que sea inmutable, o quiero que sea mutable como una lista.

Por ejemplo:
mi_tupla = (10, 20, 30)

## 2. Orden de las operaciones:
R.- Hay muchas variaciones sobre el orden de operaciones, pero por lo general en Python se sigue las reglas estándar de precedencia de operadores matemáticos (en ingles podria ser PEMDAS, pero tambien podria sería PEDMAS cuando la división va antes que la multiplicación):
1. Paréntesis
2. Exponentes
3. Multiplicación y división (de izquierda a derecha)
4. Suma y resta (de izquierda a derecha)

Por ejemplo:

resultado = 2 + 3 * 4  # Aquí primero se multiplica y luego se suma

## 3. Diccionario en Python:

R- Un diccionario es una estructura de datos que almacena pares clave-valor. Las claves deben ser únicas e inmutables (generalmente cadenas o números). Los valores pueden ser de cualquier tipo (números, cadenas, listas, etc.). Por ejemplo:

mi_diccionario = {'nombre': 'Oliver', 'edad': 27}

## 4. Diferencia entre el método ordenado y la función de ordenación:
R.- Ambos se utilizan para ordenar elementos en una lista. En lo referente a sorted(), es una función incorporada que devuelve una nueva lista ordenada sin modificar la original:

lista_original = [3, 1, 2]
lista_ordenada = sorted(lista_original), el resultado sería [1, 2, 3]


En lo referente a sort(),  es un método que ordena la lista original in situ (modifica la lista original):

lista_original.sort()


Hay que tener en cuenta que al llamar a la función de ordenación,  se cambia toda la estructura de los elementos. Sin embargo, también puede haber un momento en el que simplemente se desea pasar esto a una variable y luego tener esa variable para realizar esa ordenacion. En ese sentido, si se crea la variable sorted_list y se trata de imprimir esto, lo que va a pasar es que va a imprimir “None”  y eso es porque “sort()” no devuelve un valor.

Entonces, cuando se quiere devolver un valor, por ejemplo cuando se hace un programa,  usamos “sorted()”, el cual tiene el mismo tipo de comportamiento que sort excepto que te permite almacenar ese valor. Ese nuevo valor está ordenado dentro de una variable diferente. Lo que esto significa es que sorted no cambia los valores en su lugar por lo que la lista va a permanecer completamente intacta y cualquier otra parte del programa que no espere una lista ordenada va a poder usarla.


## 5. Operador de reasignación:
R.- El operador de reasignación (=) se utiliza para asignar un valor a una variable. Permite cambiar el valor de una variable. Por ejemplo:
x = 10
x = x + 5  # Reasignación: ahora x es 15

Esto es muy útil en el caso de trabajar con tuplas, ya que podemos aprovechar la reasignación y crear una nueva tupla y simplemente sobreescribimos el nombre de la variable y eso es muy importante, puesto que las tuplas son inmutables (no podemos cambiarlas de forma específica), pero lo que podemos hacer es crear dos objetos, agregarlos juntos, asi los estamos concatenando, luego ponerlos dentro de esta variable y simplemente va a sobreescribirlo, por ejemplo así:

x = ('Python Basics', 'Intro guide to python', 'Some python content')

x += ('published',)
