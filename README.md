# **Proyecto Bases de Datos** 

1. Agregue un campo Estado_Matrícula a la tabla Matrícula que indique si el estudiante se encuentra “En Ejecución”, “Terminado” o “Cancelado”

   ```sql
   ALTER TABLE matricula
   ADD COLUMN estado_matricula VARCHAR(20) NOT NULL;
   ```

2. Agregue a el campo edad a la tabla de Aprendices.

     ```sql
     ALTER TABLE Aprendiz 
     ADD COLUMN edad INT NOT NULL;
     ```

3. Si suponemos que los cursos tienen una duración diferente dependiendo de la ruta que lo contenga ¿qué modificación haría a la estructura de datos ya planteada?

     ```sql
     ALTER TABLE cursos
     ADD COLUMN duracion_horas INT NOT NULL;
     ```

4. Seleccionar los nombres y edades de aprendices que están cursando la carrera de electrónica.

     ```sql
     SELECT nombre_aprendiz, edad
     FROM aprendiz
     JOIN matricula on aprendiz.codigo_aprendiz = matricula.aprendiz_codigo
     JOIN ruta_aprendizaje on matricula.ruta_codigo = ruta_aprendizaje.codigo_ruta
     JOIN carrera on ruta_aprendizaje.carrera_codigo = carrera.codigo_carrera
     WHERE nombre_carrera='Electronica';
     
     +------------------------------+------+
     | nombre_aprendiz              | edad |
     +------------------------------+------+
     | Gustavo Noriega Alzate       |   26 |
     | Pedro Nell Gómez Díaz        |   27 |
     | Jairo Augusto Castro Camargo |   29 |
     | Henry Soler Vega             |   30 |
     +------------------------------+------+
     ```

5. Seleccionar Nombres de Aprendices junto al nombre de la ruta de aprendizaje que cancelaron.

     ```sql
     SELECT DISTINCT nombre_aprendiz, nombre_ruta
     FROM aprendiz
     JOIN matricula on aprendiz.codigo_aprendiz = matricula.aprendiz_codigo
     JOIN ruta_aprendizaje on matricula.ruta_codigo = ruta_aprendizaje.codigo_ruta
     WHERE estado_matricula='Cancelado';
     
     +--------------------+-------------+
     | nombre_aprendiz    | nombre_ruta |
     +--------------------+-------------+
     | Juan José Cardona  | Videojuegos |
     | Henry Soler Vega   | Robótica    |
     +--------------------+-------------+
     ```

6. Seleccionar Nombre de los cursos que no tienen un instructor asignado.

     ```sql
     SELECT nombre_curso
     FROM curso
     LEFT JOIN curso_instructor ON curso.codigo_curso = curso_instructor.curso_codigo
     WHERE curso_codigo IS NULL;
     
     +----------------------------------+
     | nombre_curso                     |
     +----------------------------------+
     | Motor de Cuatro Tiempos          |
     | Enfermedades Laborales           |
     | Higiene Postural en el Trabajo   |
     | Ergonomía                        |
     | Legislación Laboral en Colombia  |
     | Métodos de Soldadura             |
     | Buceo 2                          |
     | Riesgo Eléctrico                 |
     +----------------------------------+
     ```

7. Seleccionar Nombres de los instructores que dictan cursos en la ruta de aprendizaje “Sistemas de Información Empresariales”.

     ```sql
     SELECT DISTINCT nombre_instructor
     FROM instructor
     JOIN instructor_curso_ruta ON instructor.codigo_instructor = instructor_curso_ruta.instructor_codigo
     JOIN ruta_aprendizaje ON instructor_curso_ruta.ruta_codigo = ruta_aprendizaje.codigo_ruta
     WHERE nombre_ruta = 'Sistemas de Información Empresariales';
     +-------------------------+
     | nombre_instructor       |
     +-------------------------+
     | Marinela Narvaez        |
     | Ricardo Vicente Jaimes  |
     | Agustín Parra Granados  |
     | Nelson Raúl Buitrago    |
     | Roy Hernando Llamas     |
     +-------------------------+
     ```

8. Genere un listado de todos los aprendices que terminaron una Carrera mostrando el nombre del profesional, el nombre de la carrera y el énfasis de la carrera (Nombre de la Ruta de aprendizaje)

     ```sql
     SELECT DISTINCT nombre_aprendiz, nombre_carrera, nombre_ruta
     FROM aprendiz
     JOIN matricula ON aprendiz.codigo_aprendiz = matricula.aprendiz_codigo
     JOIN ruta_aprendizaje ON matricula.ruta_codigo = ruta_aprendizaje.codigo_ruta
     JOIN carrera ON ruta_aprendizaje.carrera_codigo = carrera.codigo_carrera
     WHERE estado_matricula = 'Terminado';
     +------------------------------+----------------+---------------------------------+
     | nombre_aprendiz              | nombre_carrera | nombre_ruta                     |
     +------------------------------+----------------+---------------------------------+
     | Gustavo Noriega Alzate       | Electrónica    | Microcontroladores              |
     | Pedro Nell Gómez Díaz        | Electrónica    | Microcontroladores              |
     | Jairo Augusto Castro Camargo | Electrónica    | Robótica                        |
     | Antonio Cañate Cortés        | Soldadura      | Soldadura Eléctrica Industrial  |
     | Daniel Simancas Junior       | Soldadura      | Soldadura Autógena Industrial   |
     +------------------------------+----------------+---------------------------------+
     ```

9. Genere un listado de los aprendices matriculados en el curso “Bases de Datos Relacionales”.

     ```sql
     SELECT DISTINCT nombre_aprendiz
     FROM aprendiz
     JOIN matricula ON aprendiz.codigo_aprendiz = matricula.aprendiz_codigo
     JOIN ruta_aprendizaje ON matricula.ruta_codigo = ruta_aprendizaje.codigo_ruta
     JOIN instructor_curso_ruta ON ruta_aprendizaje.codigo_ruta = instructor_curso_ruta.ruta_codigo
     JOIN curso ON instructor_curso_ruta.curso_codigo = curso.codigo_curso
     WHERE nombre_curso = 'Bases de Datos Relacionales';
     
     +-----------------------------+
     | nombre_aprendiz             |
     +-----------------------------+
     | Carlos Saúl Gómez           | 
     | Ana María Velázquez Parra   |
     +-----------------------------+
     ```

10. Nombres de Instructores que no tienen curso asignado.

    ```sql
    SELECT DISTINCT nombre_instructor
    FROM instructor
    LEFT JOIN curso_instructor ON instructor.codigo_instructor = curso_instructor.instructor_codigo
    WHERE curso_instructor.instructor_codigo IS NULL;
    +------------------------+
    | nombre_instructor      |
    +------------------------+
    | Pedro Nell Santamaría  |
    | Marisela Sevilla       |
    | Andrea González        |
    +------------------------+
    ```

Como parte de la evaluación académica, usted deberá elaborar, Cuatro preguntas de tipo SELECCIÓN MÚLTIPLE CON ÚNICA RESPUESTA, identificando la respuesta correcta. Someter la calidad de las preguntas al criterio del profesor en el desarrollo del proyecto.

1. **Pregunta:**
   ¿Cuál es el propósito de la cláusula `LEFT JOIN` en una consulta SQL?

   a. Se utiliza para filtrar los resultados de la tabla izquierda.

   b. Devuelve todos los registros de la tabla izquierda y los registros coincidentes de la tabla derecha.

   c. Combina solo los registros coincidentes de ambas tablas.

   d. Se utiliza para ordenar los resultados en orden descendente.

   **Respuesta correcta: b**

2. **Pregunta:**

   ¿Cuál es la función de la cláusula `ORDER BY` en una consulta SQL?

   a. Filtrar los resultados basados en condiciones especificadas.

   b. Establecer condiciones de unión entre tablas.

   c. Se utiliza para ordenar los resultados de la consulta en un orden específico.

   d. Realizar operaciones matemáticas en los datos recuperados.

   **Respuesta correcta: c**

3. **Pregunta:**
   En una tabla de base de datos, ¿qué significa una restricción de clave externa?

   a. Garantiza que los valores en una columna son únicos.

   b. Establece una relación entre dos tablas a través de una columna común.

   c. Define un conjunto de reglas para la validez de los datos en una columna.

   d. Es una columna que actúa como clave primaria en otra tabla.

   **Respuesta correcta: b**

4. **Pregunta:**
   ¿Cuál es el propósito de la cláusula `WHERE` en una consulta SQL?

   a. Filtrar los resultados basados en condiciones especificadas.

   b. Ordenar los resultados en orden alfabético.

   c. Realizar operaciones matemáticas en los datos recuperados.

   d. Seleccionar todas las columnas en la tabla.

   **Respuesta correcta: a**
