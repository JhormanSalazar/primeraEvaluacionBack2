# primeraEvaluacionBack2
Se desarrollo el parcial de backend2, corrigiendo los errores de sintaxis y documentando el proyecto.

📘 Documentación del Proyecto - Examen1Back2
✅ Descripción General

Este proyecto es construido con Spring Boot para la gestión de docentes, usuarios y cursos en un entorno educativo. Se utiliza JPA (Jakarta Persistence API) para la persistencia de datos y MySQL como sistema de base de datos.

El sistema implementa una estructura relacional con tres entidades principales: Usuario, Docente y Curso, con relaciones bien definidas entre ellas.

🔧 Mejoras y Correcciones Aplicadas

Durante la revisión del proyecto, se aplicaron diversas mejoras en las prácticas de codificación y correcciones importantes, tales como:

Se corrigieron y documentaron relaciones entre entidades usando anotaciones de JPA correctas (@OneToOne, @OneToMany, @ManyToOne).

Se implementó el uso de referencias JSON gestionadas (@JsonManagedReference y @JsonBackReference) para evitar problemas de recursividad durante la serialización.

Se mejoraron los constructores, omitiendo explícitamente el campo id, que se genera automáticamente.

Se normalizó la estructura de los nombres de columnas, claves foráneas y tablas.

Se utilizó el EnumType.STRING para facilitar el mantenimiento del campo tipoUsuario.

🧩 Entidades del Proyecto
🧑‍🏫 Docente

Representa a los profesores registrados en el sistema.

@Entity
@Table(name = "docentes")
public class Docente { ... }

Relaciones:

Uno a Muchos con Curso: Un docente puede impartir múltiples cursos.

Uno a Uno con Usuario: Cada docente está vinculado a un usuario del sistema.

Correcciones:

Se añadió la anotación @JsonManagedReference(value = "docente-curso") para gestionar correctamente la relación con Curso.

Se utilizó @JoinColumn correctamente para establecer la FK con Usuario.

📚 Curso

Representa los cursos que pueden ser asignados a los docentes.

@Entity
@Table(name = "cursos")
public class Curso { ... }

Relaciones:

Muchos a Uno con Docente: Cada curso es impartido por un único docente.

Correcciones:

Se incluyó la anotación @JsonBackReference(value = "docente-curso") para evitar bucles de serialización con Docente.

Se validó el campo nombre con restricciones nullable = false y length = 100.

👤 Usuario

Representa a los usuarios del sistema, incluyendo docentes u otros tipos de usuario.

@Entity
@Table(name = "usuarios")
public class Usuario { ... }

Relaciones:

Uno a Uno con Docente: Un usuario puede tener un perfil de docente (dependiendo del tipo de usuario).

Correcciones:

Se mejoró el uso de claves foráneas en la relación con Docente.

Se implementó el uso del enumerador TipoUsuario como EnumType.STRING.

🗃️ Base de Datos

Nombre de la base de datos: evaluacion2

Se configura automáticamente mediante el siguiente archivo application.properties:

spring.application.name=Examen1Back2

spring.datasource.url=jdbc:mysql://localhost/evaluacion2
spring.datasource.username=root
spring.datasource.password=

# Auto-actualización del esquema
spring.jpa.hibernate.ddl-auto=update


⚠️ Se recomienda definir una contraseña segura para el usuario root y no dejarla vacía en entornos de producción.

🏗️ Consideraciones Adicionales

Se recomienda separar DTOs y Entidades en el futuro para evitar exposiciones innecesarias de datos sensibles como contraseñas.

Idealmente, se deben aplicar validaciones adicionales con javax.validation o jakarta.validation en los controladores.

Se podrían implementar roles más robustos usando Spring Security para diferenciar accesos según el TipoUsuario.
