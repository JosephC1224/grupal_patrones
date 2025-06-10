Cada integrante del grupo tiene que crear un paquete con su nombre dentro del paquete **uce.project.com**
ejemplo
**uce.project.com.baraja**
dentro de este van a ir las cosas que tienen que implementar **nadie tiene que tocar el codigo fuera de su paquete**
para este projecto vamos a usar lo que esta en el paquete **uce.project.com.cat**
para crear las entidades que les voy a decir a continuación que van a hacer
**Condor:** implementar la entidad 
**User** con el username y password y la **id te tipo integer primary key autoincrement** (esto se hace con anotaciones, abajo les explico como aplicar las anotaciones)
**UserDao** una interfaz con los siguientes metodos, 
- **getUsernameById(@P("id") Integer id)**
- **insertUser(User user);**
- **updateUser(User user);**
- **deleteUser(User user);**
- **getAll();**
**Baraja** implementar la entidad
**Song** con nombre, promtId ,genero **id te tipo integer primary key autoincrement** (esto se hace con anotaciones, abajo les explico como aplicar las anotaciones)
**SongDao** una interfaz con los siguientes metodos,
- **getSongByID(@P("id") Integer id)**
- **getSongsByGender((@P("gender")String gender)**
- **filterByName(@P("name") String name)**
- **insertSong(Song user);**
- **updateSong(Song user);**
- **deleteSong(Song user);**
- **getAll()**
**Mateo** implementar la entidad
**Promt**con promt y  con  **id te tipo integer primary key autoincrement** (esto se hace con anotaciones, abajo les explico como aplicar las anotaciones)
**PromtDao**: una interfaz con los siguientes métodos:
- `getPromtByID(@P("id") Integer id)`
- `filterByWord(@P("word") String word)`
- `insertPromt(Promt promt)`
- `updatePromt(Promt promt)`
- `deletePromt(Promt promt)`
- `getAll()`

