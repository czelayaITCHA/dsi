# Fundamentos de Diseño de Bases de Datos (Relacionales y No Relacionales) y Diagramas de Clases

## 1. Diseño de Bases de Datos Relacionales

Las bases de datos relacionales están basadas en un modelo estructurado de datos, donde la información se organiza en tablas (entidades) con columnas (atributos) y filas (registros).

### 1.1 Fundamentos del Modelo Relacional

- **Entidad**: Representa una tabla en la base de datos.
- **Atributo**: Representa una columna en la tabla.
- **Clave primaria (PK)**: Identificador único de cada fila.
- **Clave foránea (FK)**: Atributo que se refiere a la clave primaria de otra entidad.
- **Relación**: Asociación entre entidades.

#### 1.1.1 Tipos de Relaciones en Bases de Datos Relacionales

En el modelo de base de datos relacional, las relaciones se establecen entre entidades a través de **claves**. Estas relaciones definen cómo los datos de una entidad están vinculados a los datos de otra. Comprender los tipos de relaciones es fundamental para diseñar bases de datos eficientes y coherentes.

Existen principalmente tres tipos de relaciones:

##### 1. Relación Uno a Uno (1:1)

En una relación uno a uno, cada fila de una tabla está relacionada con **como máximo una** fila de otra tabla, y viceversa. Esta relación es menos común que otras y a menudo indica que la información podría estar contenida en una sola tabla. Sin embargo, puede ser útil para:

* **Dividir una tabla con muchas columnas** para mejorar la legibilidad o por razones de seguridad.
* **Almacenar información opcional** que no aplica a todas las filas de la tabla principal.

**Ejemplo:**

Consideremos dos tablas: `personas` y `pasaportes`.

| Tabla `personas` |
| :--------------- |
| `id` (PK)        |
| `nombre`         |
| `apellido`       |
| `fecha_nacimiento` |

| Tabla `pasaportes` |
| :----------------- |
| `id` (PK)          |
| `numero_pasaporte` |
| `fecha_emision`    |
| `fecha_expiracion` |
| `persona_id` (FK)  |

En este ejemplo, cada persona puede tener **como máximo un** pasaporte asociado, y cada pasaporte pertenece a **exactamente una** persona. La clave foránea `persona_id` en la tabla `pasaportes` establece esta relación.

## 2. Relación Uno a Muchos (1:N)

En una relación uno a muchos, una fila de una tabla puede estar relacionada con **cero o muchas** filas de otra tabla, pero una fila de la segunda tabla solo puede estar relacionada con **una** fila de la primera tabla. Esta es una de las relaciones más comunes en las bases de datos relacionales.

**Ejemplo:**

Consideremos dos tablas: `clientes` y `contratos`.

| Tabla `clientes`|
| :-------------- |
| `id` (PK)       |
| `nombre`        |
| `tipo`          |
| `fecha_registro`|

| Tabla `contratos` |
| :---------------- |
| `id` (PK)         |
| `fecha`           |
| `numero`          |
| `monto`           |
| `cliente_id` (FK) |

En este caso, un cliente puede tener **varios** contratos (o ninguno), pero cada contrato fue adquirido por **un único** cliente. La clave foránea `cliente_id` en la tabla `contratos` apunta a la clave primaria `id` en la tabla `clientes`, estableciendo la relación.

## 3. Relación Muchos a Muchos (N:M)

En una relación muchos a muchos, varias filas de una tabla pueden estar relacionadas con **varias** filas de otra tabla. Para implementar una relación muchos a muchos en bases de datos relacionales, se necesita una **tabla intermedia** o **tabla de unión**. Esta tabla contiene claves foráneas que referencian las claves primarias de las dos tablas que se están relacionando.

**Ejemplo:**

Consideremos dos tablas: `estudiantes` y `cursos`. Un estudiante puede inscribirse en varios cursos, y un curso puede tener varios estudiantes inscritos.

| Tabla `estudiantes` |
| :------------------ |
| `id`           (PK) |
| `nombre`            |
| `apellido`          |

| Tabla `cursos`    |
| :---------------- |
| `id` (PK)         |
| `nombre_curso`    |
| `creditos`        |

Para representar la relación muchos a muchos, creamos una tabla intermedia llamada `inscripciones`:

| Tabla `inscripciones` |
| :-------------------- |
| `id`             (PK) |
| `fecha_inscripcion`   |
| `estudiante_id` (FK)  |
| `curso_id` (FK)       |


En la tabla `Inscripciones`, cada fila representa la inscripción de un estudiante en un curso específico. Las claves foráneas `id_estudiante` y `id_curso` referencian las claves primarias de las tablas `Estudiantes` y `Cursos`, respectivamente, permitiendo la relación muchos a muchos.

## Conclusión

Comprender estos tres tipos de relaciones es esencial para el diseño de bases de datos relacionales. Al identificar las relaciones correctas entre las entidades, se puede crear un modelo de datos eficiente, flexible y que refleje con precisión la realidad que se está modelando. La elección del tipo de relación impacta directamente en la estructura de las tablas y en cómo se consultan y manipulan los datos.  

## 4 - Ejemplo

![image](https://github.com/user-attachments/assets/f1454a11-ddab-4c33-b9f5-9fef56a871cd)



### 1.2 Convenciones para Nombres

- **Entidades**: En plural y minúsculas. Ej: `usuarios`, `productos`, `facturas`.
- **Atributos**: En  snake_case. Ej: `fecha_registro`, `precio_unitario`.
- **Claves primarias**: `id` . Ej: `id`.
- **Claves foráneas**: Referencia explícita. Ej: `producto_id` en la tabla `detalle_facturas`.

### 1.3 Buenas Prácticas

- Normalizar hasta 3FN (Tercera Forma Normal).
- Usar tipos de datos apropiados.
- Definir relaciones claras con restricciones de integridad.
- Evitar nombres ambiguos o reservados del sistema gestor.
- Incorporar índices para mejorar consultas.

---

## 2. Diseño de Bases de Datos No Relacionales (NoSQL)

### 2.1 Tipos de Bases de Datos NoSQL

- **Documentales** (MongoDB)
- **Clave-valor** (Redis)
- **Columnar** (Cassandra)
- **Grafos** (Neo4j)

### 2.2 Buenas Prácticas

- Diseñar en función de las consultas, no de la normalización.
- Evitar joins: embebido sobre relacionado.
- Usar claves naturales o UUID.
- Diseñar pensando en la escalabilidad horizontal.

---

## 3. Comparación entre Relacional y NoSQL

| Característica       | Relacional                       | NoSQL                            |
|----------------------|----------------------------------|----------------------------------|
| Esquema              | Fijo                             | Flexible o sin esquema           |
| Integridad           | Alta, con claves PK y FK         | Manejada por la aplicación       |
| Relaciones           | Complejas, con joins             | Embebidas o referenciadas manualmente |
| Escalabilidad        | Vertical                         | Horizontal                       |
| Ejemplo              | MySQL, PostgreSQL                | MongoDB, Redis                   |

---

## 4. Diagramas de Clases UML

### 4.1 ¿Qué es un Diagrama de Clases?

Es un tipo de diagrama UML que representa la estructura de un sistema orientado a objetos, definiendo clases, atributos, métodos y relaciones.

### 4.2 Elementos de una Clase

- **Nombre de la clase**
- **Atributos**: `- privado`, `+ público`, `# protegido`
- **Métodos (operaciones)**

![image](https://github.com/user-attachments/assets/6d055a99-acf4-4409-9a92-de1e65f61db9)


### 4.3 Relaciones Entre Clases

- **Asociación**: Una clase usa otra, es una relación semántica entre dos o más clases que especifica conexiones entre sus instancias. Es la relación más general y representa una conexión entre objetos que pueden existir independientemente el uno del otro (→)
- **Agregación**: Una clase contiene otra, pero pueden vivir separadas. (◇→)
- **Composición**: Una clase contiene otra, pero depende de ella. (⬛→)
- **Herencia**: Una clase hereda atributos y métodos de otra. (▷)
- **Dependencia**: 

### 4.3 Relaciones entre Clases

En el Diseño Orientado a Objetos, las relaciones entre clases definen cómo interactúan y colaboran los objetos de esas clases. Comprender estos tipos de relaciones es crucial para modelar sistemas complejos de manera efectiva. En UML, existen varias formas de representar estas relaciones, cada una con un significado específico.

#### 4.3.1. Asociación

La **asociación**, una clase usa a otra, es una relación semántica entre dos o más clases que especifica conexiones entre sus instancias. Es la relación más general y representa una conexión entre objetos que pueden existir independientemente el uno del otro.

* **Representación en UML:** Una línea sólida que conecta las dos clases. Opcionalmente, puede tener flechas para indicar la navegabilidad (la dirección en la que se puede acceder a la otra clase) y etiquetas para describir el rol de cada clase en la asociación. También se pueden indicar las multiplicidades en cada extremo de la línea.

**Ejemplo:**

Consideremos las clases `Persona` y `Libro`. Una persona puede leer varios libros, y un libro puede ser leído por varias personas.


---

## 5. Ejemplo de Diagrama de Clases



**Clases principales**:

- `Libro`: título, autor, isbn
- `Usuario`: nombre, email
- `Prestamo`: fecha, libro, usuario

**Relaciones**:

- Asociación entre `Usuario` y `Prestamo`
- Asociación entre `Libro` y `Prestamo`

---

## 6. Conclusión

El diseño de bases de datos (relacionales o NoSQL) y los diagramas de clases son fundamentales en el desarrollo de sistemas. Aplicar buenas prácticas y entender los principios de modelado mejora la calidad, mantenibilidad y escalabilidad del software.

