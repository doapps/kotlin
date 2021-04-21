# kotlin
DOAPPS Kotlin Style Guide

## Naming conventions
* Utilice la notación `PascalCase` si desea nombrar una `clase`.
```kt
//bad
class mainActivity {

}

//good
class MainActivity {

}
```
* Utilice la notación `PascalCase` si desea nombrar una `interface`.
```kt
//bad
interface localDataSource {

}

//good
interface LocalDataSource {

}
```
* Utilice la notación `camelCase` si desea nombrar una `función`.
```kt
//bad
fun GetPopularMovies() {

}

//good
fun getPopularMovies() {

}
```
* Utilice la notación `camelCase` si desea nombrar una `variable`.
```kt
//bad
val UserService = UserService()
val TitleHeader = "Hola mundo"

//good
val userService = UserService()
val titleHeader = "Hola mundo"

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

