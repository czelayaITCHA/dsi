# Fundamentos de Diseño de Bases de Datos (Relacionales y No Relacionales) y Diagramas de Clases

## 1. Diseño de Bases de Datos Relacionales

Las bases de datos relacionales están basadas en un modelo estructurado de datos, donde la información se organiza en tablas (entidades) con columnas (atributos) y filas (registros).

### 1.1 Fundamentos del Modelo Relacional

- **Entidad**: Representa una tabla en la base de datos.
- **Atributo**: Representa una columna en la tabla.
- **Clave primaria (PK)**: Identificador único de cada fila.
- **Clave foránea (FK)**: Atributo que se refiere a la clave primaria de otra entidad.
- **Relación**: Asociación entre entidades.

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

```plaintext
+Persona
 -nombre: String
 -edad: int
 +saludar(): void
```

### 4.3 Relaciones Entre Clases

- **Asociación**: Una clase usa otra. (→)
- **Agregación**: Una clase contiene otra, pero pueden vivir separadas. (◇→)
- **Composición**: Una clase contiene otra, pero depende de ella. (⬛→)
- **Herencia**: Una clase hereda atributos y métodos de otra. (▷)

#### Ejemplo:

```plaintext
Vehiculo <|-- Auto
Auto o---- Rueda
```

- `<|--`: Herencia
- `o----`: Agregación
- `*----`: Composición

---

## 5. Ejemplo de Diagrama de Clases

### Sistema de Biblioteca

![Ejemplo Diagrama de Clases](https://www.plantuml.com/plantuml/png/XP5BIi8m48NtESMLoKf8UifEFK2Wa8H3fWHuHaLzrdYfDtnO38hV5-0I7hhLZpRdnSPqZbAmlqZZhEvAy30ckMK-4VAYwQFURjbnIEtpkFxCkYblFTRZeuRJSCA2aK1XU2u44ZztKUSjIye23)

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

