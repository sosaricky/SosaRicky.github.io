### Tipos de datos en ruby

Number(float,integer)
String
Boolean(true,false,nil)
Symbol

Antes de empezar , un *literal* es una notación que nos permite representar un valor fijo en código.

#### Operaciones básicas con tipos de datos numéricos

- Suma,resta,multiplicación : como lo habitual.
- División : El resultado será la división entera , si queremos que nos de un float alguno de los operandos tiene que ser float.
- Módulo : El operador módulo %, no es exactamente el resto de la división. Si queremos saber el resto de la división lo seguro es usar remainder().Esto es así porque % tiene un manejo distinto cuando los operandos no son ambos positivos.Ahora bien , si ambos son positivos entonces % y remainder son equivalentes.

#### Casteo de tipos
Ruby tiene métodos para castear , por ejemplo : 

```ruby
my_variable1 = 102.45
my_variable1.to_i # Castea a Integer , ojo que trunca los decimales sin redondear

my_variable2 = 25
my_variable.to_s # Castea a String
```
#### Strings

- Se puede concatenarlos con "+". 
- Se pueden escribir entre " "  o ' ' . Pero si queremos hacer *string interpolation* debe  ser con comillas dobles.

String interpolation

```ruby
name = "Ricky"
puts "My name is #{name}"
```
Substrings

Podemos obtener substrings usando slicing
```ruby
name = "Ricky"
puts name[0..3] # El límite derecho  se incluye.
puts name[0,3] # El límite derecho no se incluye.

# [] es en realidad un alias para slice()

```
Despueś además tenemos métodos para muchas cosas como cambiar a mayúsculas,ver si incluye cierto caracter,ordenar , invertir,etc.

#### Symbols

Los symbols son una especie particular de string. Mientras que un string literal tendrá una espacio de memoria usado para cada vez que se lo cree independientemente de si ya hay otra variable con el mismo literal, el symbol en cambio siempre está guardado en la misma posición de memoria.

"Algo como un stirng , pero que no necesitamos imprimirlo , ni  modificarlo."

El uso del symbol es para cuando no necesitamos modificar el string, por ejemplo en las keys de los hash

```ruby
# Ejemplos de symbols
:iamsymbol
:"hello world"
```

Ejemplo de lo explicado
```ruby
name1 = "Ricky"
name2 = "Ricky"
# Hay dos variables que tienen el mismo valor , pero eso no significa que ambas resusan ese valor guardado en memoria , sino que cada una creo su propia copia.
# Si fuera que comparten el valor , entonces la identidad de los objetos sería la misma
name1.object_id == name2.object_id # => false
name1.equal?(name2) # => false
```

#### Valores de retorno en ruby
En ruby todo es un objeto y *toda expresión siempre retorna algo*. Si no tiene que retornar nada , entonces retorna *nil*

#### Variables boolean
true,false,nil(significa nada)

```ruby
false == nil #  => false
# si bien para comparar nil se toma como false , en realidad no son lo mismo.
```

#### Chequear igualdad

== Chequea la igualdad entre valores de objetos
.equal? Chequea si la identidad de dos objetos es la misma.


### Estructuras de datos básicas

- **Arrays** : Colección ordenada . A diferencia de otros lenguajes , puede contener elementos de distinto tipo en el mismo. Se accede por índices.Tiene los métodos típicos (a investigar cuando sea necesario , no me los acuerdo todos de memoria.)

	```ruby
	countries = ["Arg","Bra","Fra"]
	puts countries[1] # show Bra
	ages_and_names  = ["Lucas",120,"Juan",45] # Esto en otros lenguajes no va	
	```
	
-  **Hashes** : Colección no ordenada . Estructura de key,value.  Las keys suelen ser tipo symbol.
```ruby
cats = {:marte => 3, :jupiter => 2, :sol => 1}
puts cats[:sol] # 1
```

### Expressions and returns

Una expresión es cualquier cosa que puede ser evaluada. **Toda expresión en ruby siempre devuelve algo**

### Objetos.

Envíamos mensajes a los objetos mediantes operadores (. (dot) + - * ,etc).

### Variables

Podemos obtener input del usuario usando `gets`

```ruby
name = gets.chomp # chomp elimina el  \n que se agrega 
puts name
```

#### Tipos y scope de las variables
Ruby tiene distintos niveles de visibilidad para las variables según su tipo , y un concepto interesante es el de bloque

- **Variables de clase** : 
`@@name_class_variable`

>Solo son visibles por los objetos que son instancia de la clase donde se definió la variable y dentro de la misma clase en sí.
>
>Tienen que inicializarse o de lo contrario dará error al tratar de usarla.
>
>Se deben inicializar fuera de la definición de métodos.
>
>Si una instancia la modifica , entonces todas las demás verán ese cambio.
>


- **Variables de instancia**:
`@name_instance_variable`
> Son visibles por los métodos de los objetos donde está creada.
> 
> No es necesario inicializarse, por default se inicializa con *nil*.
> 


- **Variables locales**
`name_local_variable`
> Sólo visibles dentro del bloque donde se las define.
> No se necesita inicializarlas.
	
- **Variables globales**
`$name_global_variable`
>Es el tipo de variable que más visibilidad tiene.Es visible en cualquier parte del programa.
>
>Por default, si no se las inicializa , tienen el valor *nil*.
>
>No es recomendable su uso , ya que vuelve el código difícil de mantener . Al poder ser accedidas desde cualquier lado, si son modificadas se hace hard encontrar desde donde vino el cambio.


- **Constantes**

`NAME_CONSTANT_VARIABLE # Tiene que empezar con mayusculas.`
>Dependiendo de si se definen adentro o afuera de una clase o módulo , su alcance puede ser global o solo dentro de esa estructura en cuestión.
>
>No se pueden declarar dentro de definiciones de métodos.
>
>Si no se inicializa , al tratar de accederla obtendremos un error.
>
>Si tratamos de modificarla , ruby nos dará un warning

#### ¿Qué son? y formas de encontrar bloques

>Un bloque en ruby se crea cuando cuando se hace la definición de un método.Es decir , todo lo que está en su cuerpo forma parte de un bloque.

>La otra manera en que se puede encontrar un bloque es cuando nos topamos con { } o do/end inmediatamente después de la llamada a un método.

Las variables que se definen dentro de un bloque solo tienen visibilidad dentro de él.


#### Variables como referencias  o punteros.

En realidad las variables no son más que referencias o punteros a ciertas posiciones de memoria.
El valor está guardado en cierta posición de memoria y la variable es una etiqueta que guarda el valor de esa dirección de memoria.
Teniendo en cuenta esto , se debe tener cuidado de no modificar indirectamente cosas cuando hacemos operaciones que modifiquen el espacio de memoria, como los métodos bang

Ejemplo :

```ruby
a = "juan" # a apunta al espacio de memoria que guarda el valor 10
b = a  # b apunta hacia donde apunta a. 
puts "a = #{a} ; b = #{b}" # a = 10 , b = 10
```

¿Qué pasa si ahora modificamos el espacio de memoria apuntado por a?

```ruby
a = "juan" # a apunta al espacio de memoria que guarda el valor 10
b = a  # b apunta hacia donde apunta a. 
b.upcase! # método bang que modifica el espacio de memoria apuntado por b
puts "a = #{a} ; b = #{b}" # a = 10 , b = ?
# Se modificó indirectamente a través del puntero b , lo que había guardado en el lugar que apuntaba a.
```

Ahora si en cambio usamos el método upcase no bang , no modifica el espacio de memoria , por lo que b no modificará indirectamente lo que apunta "a".

```ruby
a = "juan" # a apunta al espacio de memoria que guarda el valor 10
b = a  # b apunta hacia donde apunta a. 
b = b.upcase # método  que NO modifica el espacio de memoria apuntado por b
puts "a = #{a} ; b = #{b}" # a = 10 , b = ?
```

- **Tip**
Para ver la identidad de dos objectos y saber si están apuntando al mismo espacio de memoria podemos usar ```.object_id```


### User input and output

#### Input

Usamos ```get``` combinado con `chomp` para sacar el `\n`
```ruby
puts "give me the name: "
name = gets.chomp
puts name
```

**Tip** : si queremos escribir varios comandos en la misma línea en irb usamos ";"

#### Output 

**print** : Muestra por pantalla sin agregar "\\n" .Muestra array en una sola fila.Siempre retorna nil

**puts** : Muestra por pantalla el dato y agrega un "\\n".Muestra array en varias filas. Siempre retorna nil.

>**puts**  siempre trata de convertir a string lo que se le pasa como parámetro, de manera que si le pasamos un array que tiene algún elemento *nil* , lo imprimirá como un espacio en blanco.

>Ejemplo 
>
```ruby
a = [10,nil,20,nil,40]
puts a 
# 10
# 
# 20
#
# 40
```

**p** : Muestra por pantalla de manera más raw, con caracteres de control.Retorna el objeto que se le pasó como parámetro.

**pp** (pretty print) : Muestra de manera más "linda" hash y arrays.

### Conditional logic

- **Los únicos valores que son evaluados como falso , son nil y false** . Todo lo que no sea ellos se considera verdadero . Notar que en C++ por ejemplo 0 se toma como false , pero en ruby es  true.
- **Shortcircuit** : Siempre se evalua de izquierda a derecha en las condiciones lógicas. Si el valor de verdad de lado derecho ya permite definir el resultado global de la condición , entonces lo de la izquierda no se evalua. 

#### Operadores lógicos

- Cualquier operador lógico (|| , && , !) aplicado a *valores booleanos* , dará un valor booleano , es decir , true o false. 
- Pero si aplicamos operadores lógicos a valores no booleanos , puede que el resultado no sea un booleano.

#### if

```ruby
if a > 2
	puts "mayor a 2"
else
	puts "menor a 2"
end
```

Si en el cuerpo del if hay una sola expresión a ejecutar , entonces se puede escribir en una línea
```ruby
puts "hola" if a > 2
```
#### if- elif - else

```ruby
if a > 2 
	puts "mayor a 2"
elsif a > 3
	puts "mayor a 3"
elsif a > 5
	puts "mayor a 5"
else
	puts "menor a 2"
end

# es un ejemplo inútil y estúpido

```
El else es opcional tanto en el if , como en el if  - elif.

#### Ternary operator
```ruby
a = 10
puts a > 2 ? "mayor a 2" : "menor a 2" 
```

#### unless
El bloque de código se ejecuta cuando la condición es falsa.

```ruby
a = 120
unless a > 100
	puts "something"
end	

```

#### case

Cuando encuentra la opción que matchea, inmediatamente retorna el valor del case y termina la ejecución del case statement.

```ruby
option = "red"

option_selected = case option
when "red"
	puts "rojo"
	"se eligio red"
when "blue"
	puts "blue"
	"se eligio blue"
else
	puts "otro color"
	"se eligio otro color"
end

puts option_selected
# Output del código : 
# rojo
# se eligio red
```



#### Operador ovni <=>

Compara si lo que está al lado izquierdo es menor , igual o mayor que lo de la derecha y devuelve -1 , 0 o 1 según sea el caso

```ruby
puts 4 <=> 9
puts 4 <=> 4
puts 4 <=> 1
```


#### Operadores booleanos sobre valores no booleanos

```ruby

a = "hola"
b = nil
c = 0
d = false
e = "chau"
f = 120


puts a || 0  # true
puts b && f  # false
puts !!!(d && a) # true


```


### Loops

#### while

```ruby
n = 0
while n < 4
	puts "hola"
	n += 1
end	
```

#### until
```ruby
n = 1
until n > 4
	puts "hola"
	n += 1
end
```


#### times

```ruby
n = 4
n.times do
	puts "hola"
end	
```
#### loop

```ruby
n = 1 
loop do
	puts "hola"
	if(n > 3)
		break
	end
	n += 1
end		
```

#### for
```ruby
# Para los rangos tener en cuenta  que : 
# (a..b) incluye el extremo derecho
# (a...b) no incluye el extremo derecho

for n in (0..4)
	puts "hola"
end	
```

#### each (iterador)

```ruby
names = ["john","mike","louis"]
names.each do
	|name| 
	puts "#{name}"
end	
```

#### upto

Itera hasta cierto valor de contador es alcanzado sumando

```ruby

# Hace |final_counter - initial_counter| +1 iteraciones

initial_counter = 5
final_counter = 10
initial_counter.upto(final_counter) {puts "hola"}
```

#### downto

Itera hasta cierto valor de contador es alcanzado decrementando

```ruby

# Hace |final_counter - initial_counter| +1 iteraciones


initial_counter = 7
final_counter = 3
initial_counter.downto(final_counter) {puts "hola"}
```


### Arrays

#### Crear un array

Podemos hacerlo con `Array.new(size,default_value)`
```ruby
a = Array.new(4,1)
p a # [1,1,1,1]
```

#### Acceder a un elemento de un array

- Si tratamos de acceder a un índice que no existe , retorna `nil`
	```ruby
	a = [10,6,6]
	p a[1] # 6
	p a[9] # nil
	```
#### Iterar un array

Podemos hacerlo tanto como each como con each_with_index

```ruby
a.each {|element| puts element}
a.each_with_index {|element,index| puts "a[#{index}] = #{element}"}
```

#### Agregar elemento a un array

Podemos hacerlo con push o << , ambos luego de agregar el elemento (al final) , retornan el array actualizado.
```ruby
a << 10 # [1,1,1,1,10]
a.push(9) # [1,1,1,1,10,9]
a.push(100,200) # [1,1,1,1,10,9,100,200]
```

#### Eliminar un elemento de un array

Podemos hacerlo con :

-  `my_array.delete(value)` borra todas las coincidencias y devuelve el valor borrado .
- `my_array.delete_at(index)` borra el elemento que está en la posición `index`. También devuelve el elemento eliminado.
-  `my_array.pop` borra el último elemento del arrray y lo devuelve.

```ruby
a = [1,1,1,1,10,9,4]
a.delete(1) # => 1
p a # [10,9,4]
a.delete_at(1) # => 9
p a # [10,4]
a.pop
p a # [10]
```


#### Algunos métodos para arrays

##### Obtener intersección de dos arrays
- `first_array.intersection(second_array)` 

	Devuelve un array con los elementos comunes entre `first_array`y `second_array`
```ruby
a = [19,51,22,19,8,14,6,8]
b = [8,4,2,19]
a.intersection(b) # [19,8]
```
##### Concatenar (sumar) dos arrays

La concatenación da como resultado otro array con los elementos de ambos

```ruby
a = [10,5,2]
b = [1,4,2]
a + b # [10,5,2,1,4,2]
```
##### Restar dos arrays

` a - b `tiene como resultado los elementos del array `a`, sacándole los que estén en el array `b`

```ruby
a = [19,51,22,19,8,14,6,8]
b = [8,4,2,19]
a - b # [51,22,14,6]
```

##### Otros métodos importantes
- `my_array.empty? `
- `my_array.include?(value) `
- `my_array.join(separator)` # no sepador es lo mismo que sin espacios
- `my_array.reverse`



### Hash

- Si se trata de acceder a una key que no existe retorna nil
- Para saber que la key no existia mediante un error podemos usar fetch
- Para eliminar un un elemento del hash le pasamos la key al método ```delete```
- Con los métodos `key` y `value` obtenemos respectivos arrays con las keys y values del hash.

#### Crear hash 
```ruby
# Hash vacío
my_hash = {}
# Como hash literal
my_hash = {name1:"john",name2:"louis"}
# Usando la clase Hash
my_hash = Hash.new # Hash vacío .{}
```

#### Notación con symbol para hash

Se usan generalmente symbols para las key en los hash , por lo ya visto respecto a como maneja ruby la memoria respecto a crear copias de un mismo string cada vez que una variable lo define.
Entonces en los hash hay una notación que combina el symbol y la => .

```ruby
my_hash = {:name1 => "john",:name2 => "louis"}
my_hash_pretty = {name1:"john",name2:"louis"}
```


#### Manejando key y values

Con `.keys` podemos obtener un array con todas las keys del hash.

Con `.values`podemos obtener un array con todos los values del hash

```ruby
my_hash = {:name1 => "john",:name2 => "louis"}
my_hash.keys  # [:name1,name2]
my_hash.values # ["john","louis"]
```

- ¿Qué pasa si trato de acceder a una key que no existe?
```ruby
my_hash = {:name1 => "john",:name2 => "louis"}
my_hash[:name3] # nil
```
Si la key no existe , retorna nil.

Pero si justamente existe en el hash algún value con `nil`, entonces podría existir una ambiguedad entre sí el `nil`devuelto es por no haber encontrado la key o porque si existía y su value correspondiente era `nil`.

Para evitar esto se puede usar `fetch(key,value_to_return_if_no_key)` o si queremos obtener el `KeyError` solo hacemos `fetch(key`)
```ruby
my_hash = {:name1 => "john",:name2 => "louis"}
my_hash.fetch(:name3,"key not found") # "key not found"
my_hash.fetch(:name34,"blablabla") # "blablabla"
my_hash.fetch(:name3) # KeyError
```

- Otra opción para personalizar el value que se retorna al intentar acceder a una key inexistente.
```ruby
my_hash = Hash.new("no existe")
my_hash[:name1] = "john"
my_hash[:name2] = "louis"
# En este momento el hash quedo así : {:name1 => "john",:name2 => "louis"}
# Ahora si tratamos de acceder a una key que no existe.
my_hash[:alberto] # key no existe,retorna el value por default.
# => "no existe"
```
#### Agregar y borrar elementos del hash

Podemos agregar un par key,value simplemente asignando a la nueva key un valor.Al hacerlo se retorna el value asignado a esa nueva key.
```ruby
my_hash = {name1:"john",name2:"louis"}
my_hash[:name3] = "joey"
# Ahora quedó como { name1:"john",name2:"louis",name3:"joey"}
```

Podemos eliminar un elemento con `delete(key)` y al hacerlo retorna el value que estaba asociado a la key borrada.
```ruby
my_hash = { name1:"john",name2:"louis",name3:"joey"}
my_hash.delete(:name1) # "john"
```

#### ¿Cómo iterar un hash?
Con el iterador each por ejemplo


```ruby 
my_hash = { name1:"john",name2:"louis",name3:"joey"}
my_hash.each do
|key,value|
puts "#{key}:#{value}"
end
```

#### Métodos útiles para hash

 **`.key?`**
 
Averiguar si una key determinada está en el hash 
```ruby
my_hash = { name1:"john",name2:"louis",name3:"joey"}
my_hash.key?("pepe") # false
my_hash.key?(:name1) # true
```

 **`.select { #something }`**

Aplica el hash el bloque pasado como parámetro y devuelve un hash con los pares key,value del hash original que cumplen la condición del bloque.Si ninguno lo cumple devuelve un hash vacío.

```ruby
my_hash = { name1:"john",name2:"louis",name3:"joey"}
my_hash.select { |k,v| v.length > 4 && k[-1] == "2"}
```

**`to_a`**

Convierte el hash a un representación en array , donde por cada par key,value hay un array.Y dentro de cada uno de esos array sus primer elemento es la key y el segundo el value.Devuelve esa representación y no modifica el hash original.

```ruby
my_hash = { name1:"john",name2:"louis",name3:"joey"}
my_hash.to_a # => [[:name1, "john"], [:name2, "louis"], [:name3, "joey"]]

```

 `first_hash.merge(second_hash)`
Hace un merge entre `first_hash`y `second_hash` y lo devuelve . Si en `second_hash` hay algún elemento que tiene una key que ya está en `first_hash` , entonces pisa su value con el de `second_hash`
```ruby
first_hash = {name1:"alex",name2:"ari",name3:"shubs"}
second_hash = {name4:"phix",name5:"nick",name2:"rick"}
first_hash.merge(second_hash) # {name1:"alex",name2:"rick",name3:"shubs",name4:"phix",name5:"nick"}
```

### Métodos


#### Terminología sobre métodos (obvio igual)

*Parámetros* se usa para referirse a lo que él método recibe, en términos de la definición del método.

*Argumentos* se refiere a los valores que se pasan en la llamada a un método.


#### Parámetros por default

Podemos definir parámetros que estén por default y sean usados cuando se llama sin argumentos al método.

```ruby
def saludo(nombre  = "")
	if(nombre.empty?)
		puts "Hola desconocido"
	else
		puts "Hola #{nombre}!"
	end
end
```

#### Predicate and bang methods
Predicate methods son aquellos que terminan con `?`. La idea es indicar que son métodos que devuelven un valor booleano.

`empty?`es un ejemplo

Bang methods son aquellos que modifican al objeto y se indican terminando con `!`
Por ejemplo `capitalize!` aplica el cambio al objeto permanentemente , en cambio `capitalize`devuelve un copia con la modificación del objeto y no afecta al original.

#### Return explícito e implícito

En ruby *siempre* un método devuelve el valor de la última expresión que se haya evaluado (siguiendo el orden de ejecución del bloque del método), a menos  que se ponga la instrucción explícita `return`.

#### Métodos con argumentos que son métodos

A los métodos también les podemos pasar llamadas a otros métodos como argumentos.

```ruby
def suma(a,b)
	a+b
end

def promedio_sumas(suma1,suma2)
	(suma1 + suma2)/2
end

puts promedio_sumas suma(1,2),suma(3,4)
```

#### Top level scope

Hay  métodos que son standalone y pareciera que no dependen de ser aplicados sobre ciertos objetos.Bueno en realidad, esos métodos si le pertenecen , pero al objeto anónimo que se crea cuando comienza a ejecutarse un código ruby. Ese método genera un top level scope.

Un ejemplo de este tipo de métodos es `is_a` que sirve para indicar si un objeto de cierta clase o no.
```ruby
"sddsfs".is_a?(String) # true
```


### Módulo Enumerable y algunos métodos interesantes

Enumerable es un módulo en el que hay métodos importantes

#### each

Es un método iterador, nos permite recorrer una colección y ejecutar el bloque que se le pasa como argumento, tantas veces como elementos tenga la colección.Devuelve siempre la colección original.

```ruby
people_plus_age = {john:51,louis:99,harry:19}
people_plus_age.each { |p,a| puts "Name:#{p},age:#{a}"}
# => {john:51,louis:99,harry:19}
```

#### each_with_index

Funciona de manera  similar que `each`, pero hace disponible en el bloque una variable más que guarda el índice de cada elemento de la colección.También devuelve la colección original.

```ruby
people_plus_age = {john:51,louis:99,harry:19}
people_plus_age.each_with_index { |(p,a),i| puts "Index:#{i} - Name:#{p} - age:#{a}"}
# => {john:51,louis:99,harry:19} (sale con la notación => en realidad)
```

#### map (mapea , transforma a otra cosa)

Aplica el bloque que se le pasa como parámetro a cada elemento de la colección.Devuelve **un array** con los resultados de la transformación (si queremos que sea hash usar to_h aplicado al bloque)

```ruby
people_plus_age = {john:51,louis:99,harry:19}
people_plus_age.map { |p,a| [p.capitalize,a]}.to_h
# => {John:51,Louis:99,Harry:19} (sale con la notación => en realidad)
```

#### select

Testea si cada elemento de la colección satisface la condición impuesta en el bloque pasado como argumento. Devuelve la colección pero solo con aquellos elementos que pasaron la condición.

```ruby
people_plus_age = {john:51,louis:99,harry:19}
people_plus_age.select { |p,a| a < 70 && p[0] != "j"}
# => {John:51,Louis:99,Harry:19} (sale con la notación => en realidad)
```

#### reduce

Transforma la colección en un único objeto.Se le pasa a un bloque y el resultado de ese bloque se almacena en la  variable acumulador. Luego se continua la iteración con el próximo elemento y así sucesivamente.Si no se especifica un valor inicial para el acumulador , toma el primer valor de la colección.Devuelve el valor final del acumulador


```ruby

# my_hash.reduce(valor_inicial_acumulador) { something}

people_plus_age = {john:51,louis:99,harry:19}
# Reduce para obtener la suma de edades.
people_plus_age.reduce(0){ |sum,(key,value)| sum + value}
```

Otro ejemplo :
Tenemos el array `word_list`, y queremos obtener un hash donde sus key sean las palabras de 
`word_list` y sus values la cantidad de letras de cada palabra.

```ruby
word_list = ["apple","banana","orange","potato","bean"]
word_list.reduce(Hash.new(0)) {|acum,word| acum[word] = word.length ; acum}
# => {"apple"=>5, "banana"=>6, "orange"=>6, "potato"=>6, "bean"=>4}
```
#### Métodos bang

La notación `metodo!`indica que ese método modifica el objeto sobre el que se aplica
Varios métodos de `Enumerable`tienen su versión bang, pero es mejor evitarlos por la obvia razón de perder la versión original del objeto.

#### Retornar el resultado de aplicar un método Enumerable sin usar variable 

Para no perder el resultado de un método del módulo Enumerable lo podríamos guardar en un variable , por ejemplo : 

```ruby
odd_values = {item1:1,item2:2,item3:3}
a.select{|k,v| v % 2 != 0}
# a =  
```
Pero podemos hacer algo más lindo , wrappeando el método en una función.

```ruby
def odd_values(test_hash) 
	test_hash.select{|k,v| v % 2 != 0}
end

my_hash = {a:10,b:9,c:90,d:1}
puts odd_values(my_hash)

```

### Predicate methods in Enumerable

#### any?
Devuelve un booleano indicando si al menos un elemento de la colección cumplió la condición impuesta en el bloque que se le pasa como argumento.
```ruby
a = [11,45,6]
a.any?{|n| n > 50} # false
a.any?{|n| n > 20} # true
```

#### all?
Devuelve un valor booleano que nos indica si todos los elementos de la colección cumplen la condición en el bloque que se la pasa por argumento.Si la colección que sobre la que se aplica este método está vacía , devuelve `true`por default.Tener en cuenta para evitar problemas.

```ruby
a = [11,45,6]
a.all?{ |n| n%2 == 0} # false
a.all?{|n| n > 1} # true
```


#### include?
Devuelve un booleano indicando si la colección tiene el elemento que se le pasa como argumento
true si está  y false si no está.
```ruby
a = [11,45,6]
a.include?(45) # true

h = {item1:1,item2:2,item3:3}
# En el caso de los hash el argumento es la key a saber si existe en el hash.
h.include?(:item2) # true
```
#### none?
Devuelve un booleano indicando si *ningún* elemento de la colección satifasce la condición que está definida en el bloque que se le pasa como argumento.True si ninguno cumplió , false si al
menos uno la cumplió.

```ruby
a = [11,45,6]
a.none?{ |n| n%2 == 0} # false
a.none?{|n| n > 100} # true
```

### Nested collections

Podemos generar arrays de arrays , hash de hash y la combinación de ambos.

#### Nested arrays

También llamados matrices.

##### Crear un nested array inicializado.

Tiene que hacerse de esta manera y no con `Array.new(size,default_value)`, porque `default_value` tiene que ser un inmutable.Ya que de otra manera esos default value quedarían referidos a si mismos y luego al modificar uno se modificarían todos los demás. Ver [acá](https://www.theodinproject.com/lessons/ruby-nested-collections#creating-a-new-nested-array) la explicación 


```ruby
# Ejemplo matriz 3X4
cant_filas = 3
cant_columnas = 4
nested_array = Array.new(cant_filas) { Array.new(cant_columnas)}
p nested_array
```


##### Acceder a un elemento de un nested array 

La forma de acceder a un elemento de ellos es mediante índices como sigue

```ruby
m = [
	[1,5,7],
	[3,6,1],
	[4,7,9]
]

# Accedemos el tercer elemento del segundo array.
puts m[1][3] # 1
```
- ¿Qué pasa si tratamos de acceder a un índice que no está en el array?
	Si tratamos de acceder a un índice no existente de las filas (array externo) entonces tendremos un error del tipo `NoMethod [] for NilClass`.
	En cambio , si tratamos de acceder a un índice inexistente del array anidado (interno) en ese caso si nos devolverá `nil`

Esto es un problema , pero la solución es : en vez de usar la notación `my_array[fila][col]`
usar el método `dig(fila,col)`, que en caso de que fila o columna sean índices no válidos para alguno de los arrays retornará  `nil`

```ruby
p m[1,4] # Excepcion NoMethod
p m.dig(1,4) # nil
```
#####  Agregar elementos a un nested array

Para hacerlo usamos los métodos para agregar elementos a un array en una dimensión ya vistos , solo que siendo  cuidadosos respecto a la posición donde insertamos.

```ruby
m = [
	[1,5,7],
	[3,6,1],
	[4,7,9]
]

# Vamos a agregar un elemento a la segunda fila.
m[1].push(10)
p m # [[1, 5, 7], [3, 6, 1, 10], [4, 7, 9]]

```

##### Eliminar un elemento de un nested array

Mismos métodos que para eliminar un elemento de un array en una dimensión.
```ruby
# Eliminamos el segundo elemento de la primera fila.
m[0].delete_at(1) # con delete(value) borramos por valor y no índice. 
p m # [[1, 7], [3, 6, 1, 10], [4, 7, 9]]
```

##### Iterar sobre un nested array

Se usan los iteradores `each`y `each_with_index` prestando atención a que se tienen que usar uno por cada fila y por cada columna.

```ruby
m = [
	[1,5,7],
	[3,6,1],
	[4,7,9]
]

# vamos a iterar para mostrar fila x : col 1 : col 2 : col 3 , etc
m.each_with_index do
	|fila,indice| 
	puts "\nfila #{indice} "
	fila.each_with_index {|columna,indice|  print "col #{indice}:#{columna} "
	}
end
```

#### Nested hashes

Es anidar hashes , hash de hashes. Las formas de manipularlos se basan en los métodos ya vistos.

##### Crear nested hash

```ruby
nested_hash = {item1:{a:1,b:2,c:3},item2:{d:4,e:5,f:6}}
```

##### Agregar elementos a un nested hash

```ruby
nested_hash = {item1:{a:1,b:2},item2:{d:3,e:4}}
nested_hash[:item1][:new_item] = 99
p nested_hash # {:item1=>{:a=>1, :b=>2, :new_item=>99}, :item2=>{:d=>3, :e=>4}}
```

##### Eliminar elementos de un nested hash

```ruby
nested_hash = {item1:{a:1,b:2,new_item:99},item2:{d:3,e:4}}

# Eliminamos la primer key del primer hash
nested_hash[:item1].delete(:a)
p nested_hash # {:item1=>{:b=>2,:new_item=>99}, :item2=>{:d=>3, :e=>4}}
```
##### Iterar un nested hash
```ruby
nested_hash = {item1:{a:1,b:2,new_item:99},item2:{d:3,e:4}}
nested_hash.each do
	|key,hash_value|
	puts "#{key}"
	hash_value.each {|key,value| puts "#{key}/#{value}"}
	puts "-------" 	
end	
```

##### Ejemplos de nested hashes y métodos de Enumerable

```ruby
langs =
{
 ruby: { facts: ['fact 0', 'fact 1'],
		 initial_release: 'December 25, 1996',
		 is_beautiful?: true },

 javascript: { facts: ['fact 0', 'fact 1'],
			   initial_release: 'December 4, 1995',
			   is_beautiful?: false }
}

# Se nos pide que a partir de un lang_name y un fact_index obtengamos el fact correspondiente. Si  lang_name no es una key de langs, retornar nil.

# Test
lang_name = :python
fact_index = 0

# Solución 
resultado = langs.key?(lang_name) ? langs[lang_name][:facts][fact_index] : nil
# => nil
```

```ruby
# Take langs and return a hash containing only lang which have the key/value pair { is_beautiful?: true } listed in their information

langs.select { |lang,info_lang| info_lang.include?(:is_beautiful?) && info_lang[:is_beautiful?] == true}
# => {:ruby=>
#  {:facts=>["fact 0", "fact 1"],
#   :initial_release=>"December 25, 1996",
#   :is_beautiful?=>true}}

```



