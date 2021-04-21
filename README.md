# kotlin
DOAPPS Kotlin Style Guide

# Table of Contents

1. [Naming conventions](#naming-conventions)
1. [Espaciados](#espaciados)
1. [Saltos de linea](#saltos-de-linea)

## Naming conventions

### Clases

* Utilice la notación `PascalCase` si desea nombrar una `clase`.

```kt
//bad
class mainActivity {

}

//good
class MainActivity {

}
```
* No utilice `verbos` si desea nombrar una `clase`.
* Tambien evite usar `Manager`, `Processor`, `Data`, `Info` en el nombre de la `clase`.
```kt
//bad
class GetDataConverters {

}

//good
class TypeConverters {

}
```

### Interfaces

* Utilice la notación `PascalCase` si desea nombrar una `interface`.
```kt
//bad
interface localDataSource {

}

//good
interface LocalDataSource {

}
```
### Funciones

* Utilice la notación `camelCase` si desea nombrar una `función`.
```kt
//bad
fun GetPopularMovies() {

}

//good
fun getPopularMovies() {

}
```
* Utilize  `verbos` al nombrar un `función` que demuestre el motivo de su creación.

```kt
//bad
fun stringToList() {

}

//good
fun convertStringToList() {

}
```
* No se recomienda usar  `verbos` muy rebuscados, esto complicará al entendimiento de su código.
```kt
//bad
fun expungeMovieById() {

}

//good
fun deleteMovieById() {

}
```
### Variables

* Utilice la notación `camelCase` si desea nombrar una `variable`.
```kt
//bad
val UserService = UserService()
val TitleHeader = "Hola mundo"

//good
val userService = UserService()
val titleHeader = "Hola mundo"

```
* Utilice palabras que describan las intenciones si desea nombrar una `variable` .
```kt
//bad
val a = 10
var b = 1
for(x in 1..a){
    b *= x
}
println("El factorial de $a es : $b")

//good
val numFactorial = 10

var resultFactorial = 1

for(index in 1..numFactorial){
    resultFactorial *= index
}

println("El factorial de $numFactorial es : $resultFactorial")
```

## Espaciados
Al igual que un parrafo de un libro, siempre agregar, un espacio luego de una coma `','`  

### Clases

* Agregar un espacio al terminar de definir el nombre de la clase
```kt
//bad
class MainActivity{

}

//good
class MainActivity {

}
```
* Para `clases con constructores`, agregar un espacio luego de los `:` para definir el tipo y luego de las `,`
```kt
//bad
class MainActivity(val user:User,val repository: Repository){

}

//good
class MainActivity(val user: User, val repository: Repository) {

}
```
* Para `clases con lambdas`, agregar un espacio antes y despues de `->`
```kt
//bad
class MainActivity(val user:User,private val listener: (User)->Unity){

}

//good
class MainActivity(val user: User, private val listener: (User) -> Unity) {

}
```
* Para `Herencias`, agregar un espacio antes y despues de los `:`
```kt
//bad
class MainActivity: AppCompatActivity() {

}

//good
class MainActivity : AppCompatActivity() {

}
```

### Objetos
* Para `Objetos con argumentos` agregar un espacio luego de los `:` para definir el tipo 
```kt
//bad
val userService = UserServie(val context:Context)

//good
val userService = UserServie(val context: Context)

```

### Funciones
* Para `Funciones con valores de retorno explicito` agregar un espacio luego de los `:` para definir el tipo de retorno
```kt
//bad
private fun getFilteredItems(filter: Filter) : List<MediaItem> {
    
}

//good
private fun getFilteredItems(filter: Filter): List<MediaItem> {
    
}

```
### Listas

* Agregar un espacio luego de cada valor dentro de una lista
```kt
//bad
val numbers = listOf(1,2,3,4,5,6)

//good
val numbers = listOf(1, 2, 3, 4, 5, 6)
```
## Saltos de linea
* Agregar un salto de linea luego de cada bloque de función
```kt
//bad
class MainViewModel : ViewModel() {
    fun updateItems(filter: Filter = Filter.None) {
        viewModelScope.launch {
            // ..
        }
    }
    private fun getFilteredItems(filter: Filter): List<MediaItem> {
        return MediaProvider.getItems().let { media ->
            when (filter) {
               // ..
            }
        }
    }
    fun onMediaItemClicked(mediaItem: MediaItem) {
        // ..
    }
}

//good
class MainViewModel : ViewModel() {
    fun updateItems(filter: Filter = Filter.None) {
        viewModelScope.launch {
            // ..
        }
    }

    private fun getFilteredItems(filter: Filter): List<MediaItem> {
        return MediaProvider.getItems().let { media ->
            when (filter) {
               // ..
            }
        }
    }

    fun onMediaItemClicked(mediaItem: MediaItem) {
        // ..
    }
}

```
* Agregar un salto de linea despues de cada bloque de código
```kt
//bad
fun onCreate(itemId: Int) {
    if(itemId == 0) {
        return
    }
    holder.itemView.setOnClickListener {
        listener(itemId)
    }
}

//good
fun onCreate(itemId: Int) {
    if(itemId == 0) {
        return
    }

    holder.itemView.setOnClickListener {
        listener(itemId)
    }
}
```
* Agregar saltos de linea para definiciones largas
```kt
//bad
class MediaAdapter(items: List<Item> = emptyList(), users: List<User> = emptyList()) : RecyclerView.Adapter<MediaAdapter.ViewHolder>() {

}
//good
class MediaAdapter(items: List<Item> = emptyList(), users: List<User> = emptyList()) 
    :RecyclerView.Adapter<MediaAdapter.ViewHolder>() {

}
```
* Agregar saltos de linea para muchos parametros.
```kt
//bad
class MediaAdapter(items: List<Item> = emptyList(),
    users: List<User> = emptyList(),
    jobs: List<Job> = emptyList()) : RecyclerView.Adapter<MediaAdapter.ViewHolder>() {

}
//good
class MediaAdapter(
    items: List<Item> = emptyList(),
    users: List<User> = emptyList(),
    jobs: List<Job> = emptyList()
) : RecyclerView.Adapter<MediaAdapter.ViewHolder>() {

}
```

## Número de lineas de código y parametros
¿Se imaginan una Clase con mas de 2000 o 3000 lineas de código? Lo mas probable esque esta clase este violando mas de un principio SOLID y en particular el de responsabilidad unica. Las clases, archivos y funciones con muchas lineas de código son dificiles de leer y por lo tanto dificiles de mantener.

En nuestro esfuerzo de encontrar datos o estudios que respalden cuantas lineas como maximo debería tener una clase, archivo ó función, encontramos una opinion de un Google Developer Expert en Android - Antonio Leiva, Antonio nos comparte números referentes según su basta experiencia en el mundo Android, para esta guia lo llamaremos el metodo 666 y se establece de la siguiente forma:

- Clases -> `600` lineas de código como máximo
- Funciones -> `60` lineas de código como máximo
- Parametros -> `6` parametros como máximo

Desde luego estos números son relativos, si pasamos estos números se recomienda verificar si la clase, función o los numeros de parametros presentes pueden ser refactorizados. Recordemos que es buena practica mantener la responsabilidad única tanto en clases como funciones.
