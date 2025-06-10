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




# 1. Creación de Entities (Entidades)
Las entidades representan tablas en tu base de datos. Para crear una:

- Anota la clase con `@Entity`: Especifica el nombre de la tabla.
- Define los campos: Cada campo representa una columna en la tabla.
- Anota los campos:
  - `@ColumnInfo` para columnas normales
  - `@PrimaryKey` para la clave primaria
- Usa Lombok (opcional pero recomendado): Para generar getters, constructores, etc.

## Ejemplo completo de Entity:

```java
package com.tuapp.entities;

import uce.project.com.cat.anotations.Entity;
import uce.project.com.cat.anotations.PrimaryKey;
import uce.project.com.cat.anotations.ColumnInfo;
import lombok.*;

@Getter
@ToString
@Builder
@NoArgsConstructor
@AllArgsConstructor
@Entity("Producto") // Nombre de la tabla en la base de datos
public class Producto {
    @ColumnInfo(name = "id")
    @PrimaryKey(autoIncrement = true)
    private Integer id;
    
    @ColumnInfo(name = "nombre", params = "255")
    private String nombre;
    
    @ColumnInfo(name = "precio")
    private Double precio;
    
    @ColumnInfo(name = "stock")
    private Integer stock;
    
    @ColumnInfo(name = "activo")
    private Boolean activo;
}

## 2. Creación de DAOs (Data Access Objects)

Los DAOs (Data Access Objects) son interfaces que definen las operaciones CRUD sobre las entidades.

### Configuración básica:

- Anota la interfaz con `@Dao`
- Define métodos con las anotaciones adecuadas:
  - `@Query` para consultas SQL personalizadas
  - `@Insert` para operaciones de inserción
  - `@Update` para operaciones de actualización
  - `@Delete` para operaciones de eliminación
- Usa `@P` para parámetros en consultas nombradas

### Ejemplo completo de DAO:

```java
package com.tuapp.daos;

import uce.project.com.cat.anotations.*;
import com.tuapp.entities.Producto;
import java.util.List;

@Dao
public interface ProductoDao {
    // Consulta todos los productos
    @Query("SELECT * FROM Producto")
    List<Producto> getAll();
    
    // Consulta productos activos
    @Query("SELECT * FROM Producto WHERE activo = true")
    List<Producto> getActivos();
    
    // Consulta por ID
    @Query("SELECT * FROM Producto WHERE id = :id")
    List<Producto> getById(@P("id") Integer id);
    
    // Consulta por nombre (usando LIKE)
    @Query("SELECT * FROM Producto WHERE nombre LIKE :nombre")
    List<Producto> searchByName(@P("nombre") String nombre);
    
    // Insertar producto
    @Insert
    boolean insert(Producto producto);
    
    // Actualizar producto
    @Update
    boolean update(Producto producto);
    
    // Eliminar producto
    @Delete
    boolean delete(Producto producto);
}
#Asi se agregan las entidades y los daos a la AppDatabase

@Database(entities = {User.class, Product.class, Song.class}) // parar aqui las entidades ejemplo Song.class
public interface AppDataBase {
    public UserDao userDao(); // funcion para acceder al dao
    public ProductDao productDao(); //otro ejemplo
}
