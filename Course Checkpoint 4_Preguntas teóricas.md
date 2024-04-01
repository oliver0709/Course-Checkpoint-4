# Course Checkpoint 4. Preguntas teóricas



## 1. Diferencia entre una lista y una tupla:
R. En Python, tanto las listas como las tuplas son estructuras de datos utilizadas para almacenar colecciones de elementos. La principal diferencia radica en su mutabilidad y sintaxis. Las listas son mutables, lo que significa que se puede cambiar, agregar o eliminar elementos después de haber creado la lista. Estas se definen usando corchetes [ ]. Por otro lado, las tuplas son inmutables, lo que significa que una vez creada una tupla, no puedes cambiar sus elementos. Estas se definen usando paréntesis ( ). 

Las listas pueden contener elementos de diferentes tipos de datos como enteros, float, cadenas de caracteres, entre otros. Una lista inclusive puede contener otra lista, además, la cantidad de elementos de una lista se puede modificar removiendo o añadiendo elementos. Por ejemplo:
```python
calificaciones = [10,9,8,7.5,9]
nombres = ["Ana","Juan","Sofía","Pablo","Tania"]
mezcla = [True, 10.5, "abc", [0,1,1]]
```
Las listas son iterables y por tanto se puede acceder a sus elementos mediante indexación:
```python
nombres[2]
'Sofía'
nombres[-1]
'Tania'
```
Se tiene la posibilidad de agregar elementos, para ello se puede usar tanto el método _extend()_, el cual agrega varios elementos al final de la lista, como el método _append()_, que agrega un elemento al final de la lista:
```python
nombres.append("Antonio")
nombres.append("Ximena")
print(nombres)
['Ana', 'Juan', 'Sofía', 'Pablo', 'Tania', 'Antonio', 'Ximena']
```
El método _remove()_ elimina un elemento de una lista:
```python
nombres.remove("Ana")
print(nombres)
['Juan', 'Sofía', 'Pablo', 'Tania', 'Antonio', 'Ximena']
```

Para visualizar la diferencia en inmutabilidad y por ende en el funcionamiento del código de listas y tuplas, veamos las siguientes diferencias en Python:

```python
# Lista
lista = [1, 2, 3]
lista.append(4)  # Esto es posible
lista[0] = 0     # Esto también es posible

# Tupla
tupla = (1, 2, 3)
tupla.append(4)  # Esto arrojará un error, las tuplas son inmutables
tupla[0] = 0     # Esto también arrojará un error

```
En lo referente a las tuplas, cabe señalar que son más eficientes que las listas en términos de espacio y tiempo de ejecución. 

En ese sentido, en lo concerniente a la compilación, Python reconoce y evalúa las tuplas como expresiones constantes en el momento de compilación, en vez de en la ejecución, esto es conocido como Constant Folding. Asi mismo, hay diferencia en el copiado, cuando se quiere copiar una lista, Python vuelve a reservar memoria para crear una nueva lista. En el caso de las tuplas, debido a su inmutabilidad, no se copia, simplemente se crea una referencia shallow copy. Vamos a demostrarlo:
```python
lista_1 = [1,2,3,4,5]
lista_2 = list(lista_1)
print("Lista copiadas: ", hex(id(lista_1)), hex(id(lista_2)))

tupla_1 = (1,2,3,4,5)
tupla_2 = tuple(tupla_1)
print("Tupla copiada:  ", hex(id(tupla_1)), hex(id(tupla_2)))

#Salida:

Lista copiadas:  0x7f9cc80bb960 0x7f9cc17a9500
Tupla copiada:   0x7f9cc8101bf0 0x7f9cc8101bf0
```
Al copiar la lista se encuentran en distintas posiciones de memoria, sin embargo la tupla está en la misma posición de memoria. Esto también tiene un impacto en los tiempos de ejecución:
```python
from timeit import timeit

timeit("tuple((1,2,3,4,5))", number=5_000_000)
timeit("list((1,2,3,4,5))", number=5_000_000)

#Salida

Lista copiadas:  0.5346233499985829
Tupla copiadas:  0.3198905820026994
```

En lo concerniente al almacenamiento, para una tupla es exacto, es decir, Python reserva el espacio justo y necesario para almacenar una tupla, ya que es inmutable. En las listas es distinto, Python reserva más espacio del necesario para una lista, lo que se conoce como Overallocation y pre-allocate con el objetivo de optimizar la entrada de elementos en dicha lista. Por ello, Python en este caso utiliza un algoritmo que fijándose en el tamaño de la lista, calcula cuanto espacio más va a reservar. Así si por ejemplo usamos .append() y la lista crece, nos evitamos tener que volver a reservar espacio para introducir el elemento, ya que dicho espacio está previamente reservado.

Por otro lado, cuando se trabaja con Python en campos como machine learning, muchas veces se debe decidir si se quiere tener mayor control sobre las estructuras de datos, así que cuando se trata de elegir entre una tupla y una lista, uno debe preguntarse si se trata de una estructura de datos que tengo que cambiar o es algo que quiero mantener. En otras palabras, si quiero que sea inmutable, o quiero que sea mutable como una lista. 

En ese sentido, por lo general se suele preferir las listas cuando se necesita una colección de elementos que se pueda cambiar a lo largo del tiempo, mientras que las tuplas son útiles para datos que no deben modificarse una vez definidos, como coordenadas geográficas o claves de diccionario constantes.


## 2. Orden de las operaciones:

R. El orden de las operaciones en Python sigue las reglas estándar de las matemáticas, donde primero se resuelven las operaciones entre paréntesis, luego las de exponentes, seguidas de multiplicaciones y divisiones, y finalmente sumas y restas. Este orden se conoce como PEMDAS, se suele utilizar el acrónimo PEMDAS con mas prepondarancia en Estados Unidos; pero tambien podria sería PEDMAS cuando la división va antes que la multiplicación, lo cual es mas utilizado en Reino Unido y otro paises. Este último acrónimo es similar a BODMAS, cuyas reglas establecen tambien que la división y la multiplicación deben realizarse antes que la suma y la resta en cualquier operación matemática, en inglés sería lo siguiente:

- B – Brackets: Used to Solve expressions within brackets first.
- O – Orders: Evaluate expressions with exponents or roots next.
- D – Division: Perform division from left to right.
- M – Multiplication: Perform multiplication from left to right.
- A – Addition: Perform addition from left to right.
- S – Subtraction: Perform subtraction from left to right.

En ese contexto, podemos ver que esto suscita múltiples debates en la comunidad de estudios matemáticos. De forma general, todas representan el mismo orden de operaciones y las diferencias se deben en gran medida a preferencias regionales. Por tanto, podriamos seguir el siguiente orden:

1. Paréntesis
2. Exponentes
3. Multiplicación y división (de izquierda a derecha)
4. Suma y resta (de izquierda a derecha)

A continuación, un ejemplo de código que sigue las reglas de PEMDAS:

```python
resultado = (2 + 3) * 4 ** 2 / 2 - 5

# Desglose según PEMDAS
# 1. Paréntesis
#    (2 + 3) se evalúa primero
#    resultado = (5) * 4 ** 2 / 2 - 5

# 2. Exponentes
#    4 ** 2 se evalúa después
#    resultado = 5 * 16 / 2 - 5

# 3. Multiplicación y División (de izquierda a derecha)
#    5 * 16 se realiza antes de la división porque aparece primero de izquierda a derecha
#    resultado = 80 / 2 - 5
#    Luego, 80 / 2
#    resultado = 40 - 5

# 4. Suma y Resta (de izquierda a derecha)
#    Finalmente, 40 - 5
   
print(resultado)  # Debería imprimir 35
```

Esto nos demuestra cómo Python aplica las reglas de PEMDAS para producir el resultado esperado de la expresión. Es crucial entender y aplicar correctamente estas reglas cuando se escriben expresiones matemáticas complejas en Python para asegurar que se obtengan los resultados deseados.


## 3. Diccionario en Python:

R. En Python, un diccionario es una estructura de datos que almacena pares clave-valor (key-value), donde cada clave es única dentro del diccionario y está asociada a un valor específico. Los diccionarios son mutables, lo que significa que puedes modificar, agregar o eliminar elementos después de haber creado el diccionario. Se definen utilizando llaves {} y separando cada par clave-valor por dos puntos :.

Por ejemplo:
```python
mi_diccionario = {'nombre': 'Oliver', 'edad': 27, 'ciudad': 'Madrid'}
```

Para crear un diccionario en Python, tambien se puede usar dict() y luego introducir los pares key: value entre paréntesis. Por ejemplo:
```python
d2 = dict([
      ('Nombre', 'Sara'),
      ('Edad', 27),
      ('Documento', 1003882),
])
print(d2)
#{'Nombre': 'Sara', 'Edad': '27', 'Documento': '1003882'}
```

También es posible usar el constructor dict() para crear un diccionario.
```python
d3 = dict(Nombre='Sara',
          Edad=27,
          Documento=1003882)
print(d3)
#{'Nombre': 'Sara', 'Edad': 27, 'Documento': 1003882}
```

Algunas propiedades de los diccionarios en Python son las siguientes:

- Son dinámicos, pueden crecer o decrecer, se pueden añadir o eliminar elementos.
- Son indexados, los elementos del diccionario son accesibles a través del key.
- Y son anidados, un diccionario puede contener a otro diccionario en su campo value.
  

Para acceder a sus elementos, se puede hacerlo con [] o también con la función get()

```python
print(d1['Nombre'])     #Sara
print(d1.get('Nombre')) #Sara
```
Para modificar un elemento basta con usar [] con el nombre del key y asignar el valor que queremos.

```python
d1['Nombre'] = "Laura"
print(d1)
#{'Nombre': Laura', 'Edad': 27, 'Documento': 1003882}
```

Si el key al que accedemos no existe, se añade automáticamente.
```python
d1['Direccion'] = "Calle 123"
print(d1)
#{'Nombre': 'Laura', 'Edad': 27, 'Documento': 1003882, 'Direccion': 'Calle 123'}
````

Ademas, los diccionarios se pueden iterar de manera muy similar a las listas u otras estructuras de datos. Para imprimir las claves, se puede hacer de la siguiente manera:
```python

for x in d1:
    print(x)
#Nombre
#Edad
#Documento
#Direccion
```
Se puede imprimir también solo los valores:

```python
for x in d1:
    print(d1[x])
#Laura
#27
#1003882
#Calle 123
```
O si queremos imprimir la clave y el valor a la vez:

```python
for x, y in d1.items():
    print(x, y)
#Nombre Laura
#Edad 27
#Documento 1003882
#Direccion Calle 123
```
En definitiva, los diccionarios son muy útiles para almacenar información estructurada, como datos de usuarios, configuraciones de aplicaciones o cualquier conjunto de datos que requiera acceso eficiente mediante una clave única.



## 4. Diferencia entre el método ordenado y la función de ordenación:

R.- Ambos se utilizan para ordenar elementos en una lista. En lo referente a sorted(), es una función incorporada que devuelve una nueva lista ordenada sin modificar la original. En lo referente a sort(), es un método que ordena la lista original in situ. Por ejemplo:
```python
lista = [3, 1, 2]
nueva_lista = sorted(lista)  # Devuelve una nueva lista ordenada
print(nueva_lista)  # Salida: [1, 2, 3]

lista.sort()  # Ordena la lista original
print(lista)  # Salida: [1, 2, 3]
```


Hay que tener en cuenta que al llamar a la función de ordenación, se cambia toda la estructura de los elementos. Sin embargo, también puede haber un momento en el que simplemente se desea pasar esto a una variable y luego tener esa variable para realizar esa ordenacion. En ese sentido, si se crea la variable sorted_list y se trata de imprimir esto, lo que va a pasar es que va a imprimir “None”  y eso es porque “sort()” no devuelve un valor, tal y como se puede apreciar a continuacion:
```python
my_list = [3, 1, 2]
sorted_list = my_list.sort()
print(sorted_list)  # Salida: None
```

Entonces, cuando se quiere devolver un valor, por ejemplo cuando se hace un programa,  usamos “sorted()”, el cual tiene el mismo tipo de comportamiento que _sort_ excepto que te permite almacenar ese valor. Ese nuevo valor está ordenado dentro de una variable diferente. Lo que esto significa es que _sorted_ no cambia los valores in-place por lo que la lista va a permanecer completamente intacta y cualquier otra parte del programa que no espere una lista ordenada va a poder usarla.

Otra diferencia es que el método list.sort() solo aplica para las listas. En contraste, la función sorted() acepta cualquier iterable. Por ejemplo:

```python
x= sorted({1: 'D', 2: 'B', 3: 'B', 4: 'E', 5: 'A'})
print(x)  #Devuelve [1, 2, 3, 4, 5]
```
Por otra parte, ambos list.sort() y sorted() tienen un parámetro key para especificar una función (u otra invocable) que se llamará en cada elemento de la lista antes de hacer comparaciones.

Por ejemplo, aquí hay una comparación de cadenas que no distingue entre mayúsculas y minúsculas:

```python
x = sorted("This is a test string from Oliver".split(), key=str.casefold)
print(x)  #Devuelve ['a', 'from', 'is', 'Oliver', 'string', 'test', 'This']
```

El valor del parámetro key debe ser una función (u otra invocable) que tome un solo argumento y retorne una clave para usar con fines de clasificación. Esta técnica es rápida porque la función de la tecla se llama exactamente una vez para cada registro de entrada.


Asi mismo, ambos list.sort() y sorted() aceptan un parámetro reverse con un valor booleano. Esto se usa para marcar tipos descendentes. Por ejemplo, para obtener los datos de unos estudiantes en orden inverso de edad:

```python
student_tuples = [
  ('john', 15),
  ('jane', 12),
  ('dave', 10),
]

st=sorted(student_tuples, reverse=True)
print(st)  #Devuelve [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
```
En definitiva, es importante elegir el método adecuado según las necesidades específicas del programa. Si se desea conservar la lista original y obtener una nueva lista ordenada, uno deberia utilizar sorted(). Si se prefiere ordenar la lista existente sin crear una copia, deberia usarse sort().

## 5. Operador de reasignación:
R. Un operador de reasignación en Python se utiliza para cambiar el valor de una variable existente. El operador de reasignación más común es +=, que añade el valor a la variable y luego asigna el resultado a la misma variable. También existen otros operadores de reasignación como -= para resta, *= para multiplicación, /= para división, etc. A continuacion, podemos ver algunos de los casos mas comunes:

```python
a=7; b=2
print("Operadores de asignación")
x=a; x+=b;  print("x+=", x)  # 9
x=a; x-=b;  print("x-=", x)  # 5
x=a; x*=b;  print("x*=", x)  # 14
x=a; x/=b;  print("x/=", x)  # 3.5
x=a; x%=b;  print("x%=", x)  # 1
x=a; x//=b; print("x//=", x) # 3
x=a; x**=b; print("x**=", x) # 49
x=a; x&=b;  print("x&=", x)  # 2
x=a; x|=b;  print("x|=", x)  # 7
x=a; x^=b; print("x^=", x)   # 5
x=a; x>>=b; print("x>>=", x) # 1
x=a; x<<=b; print("x<<=", x) # 28
```

En general, dichos operadores son útiles cuando se quiere actualizar el valor de una variable sin tener que referenciarla repetidamente. Es una práctica común y concisa para escribir código más legible y eficiente.

Esto tambien es muy útil en el caso de trabajar con tuplas, ya que podemos aprovechar la reasignación y crear una nueva tupla y simplemente sobreescribimos el nombre de la variable y eso es muy importante, puesto que las tuplas son inmutables (no podemos cambiarlas de forma específica), pero lo que podemos hacer es crear dos objetos, agregarlos juntos, asi los estamos concatenando, luego ponerlos dentro de esta variable y simplemente va a sobreescribirlo, por ejemplo así:
```python
y = ('Python Basics', 'Intro guide to python', 'Some python content')

y += ('published',)
print(y) #Devuelve ('Python Basics', 'Intro guide to python', 'Some python content', 'published')
```
De igual forma, se podría emplear sobre una lista, tal y como se puede apreciar a continuacion:
```python
x=[1,2,3] 
x+=[4,5]  # Se aplica el operador sobre otra lista
print(x)  # Y el resultado es [1, 2, 3, 5, 6]
```

Es muy importante, que si x es una lista, no podemos aplicar el operador += con un elemento que no sea una lista, como por ejemplo, un número. El siguiente código daría error porque el operador no esta definido para un elemento lista y otro entero:
```python
x=[1,2,3] #
#x+=3     # ERROR! TypeError
```
