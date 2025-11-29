# 📝 1 Simulacro Examen Tipo Test: Diseño de Bases de Datos (Conceptual, Lógico y Físico (DDL))

## Parte I: Selección Única

**1. En el contexto de las propiedades dinámicas del Modelo ER, ¿cuál es la diferencia principal entre una operación y una transacción?**
   a. Una operación involucra a varias entidades, mientras que una transacción solo a una.
   b. Una operación es una acción indivisible, mientras que una transacción es una secuencia de operaciones que se ejecuta de forma atómica (todas o ninguna).
   c. Las transacciones son solo de lectura (SELECT), mientras que las operaciones modifican datos.
   d. No hay diferencia, son sinónimos en el diseño conceptual.

**2. Si en un diagrama ER vemos un atributo conectado a una entidad mediante un óvalo con borde punteado, ¿qué significa?**
   a. Es un atributo identificador secundario.
   b. Es un atributo opcional (puede ser nulo).
   c. Es un atributo derivado (su valor se calcula a partir de otros datos).
   d. Es un atributo multivaluado.

**3. En una relación con cardinalidad `(0, 1)` en un extremo y `(1, N)` en el otro. ¿Qué significa la cardinalidad `(0, 1)` para esa entidad?**
   a. Que la entidad participa obligatoriamente en la relación una vez.
   b. Que una ocurrencia de la entidad puede no relacionarse con ninguna, o como máximo con una ocurrencia de la otra entidad.
   c. Que la entidad participa opcionalmente y puede relacionarse con muchas.
   d. Que es una entidad débil.

**4. ¿Cómo se denomina a la restricción en una jerarquía (EER) donde una ocurrencia de la superclase NO puede pertenecer a más de una subclase a la vez?**
   a. Solapada (Overlap).
   b. Parcial.
   c. Disjunta.
   d. Total.

**5. ¿Cuál es la principal motivación para utilizar una Agregación en el diseño conceptual?**
   a. Para convertir atributos multivaluados en entidades.
   b. Para poder relacionar una relación existente (tratándola como una entidad) con otra entidad nueva, evitando relaciones ternarias complejas.
   c. Para definir claves primarias compuestas.
   d. Para representar herencia de atributos.

**6. En el Modelo Relacional, si tenemos una tabla `EMPLEADO` con los atributos `DNI` y `NumSeguridadSocial`, y elegimos `DNI` como Clave Primaria. ¿Qué tipo de clave es `NumSeguridadSocial`?**
   a. Clave Foránea.
   b. Clave Alternativa.
   c. Clave Subrogada.
   d. Clave Débil.

**7. Según las reglas de integridad del modelo relacional, ¿qué afirmación es correcta respecto a las Claves Ajenas (FK)?**
   a. Nunca pueden contener valores nulos (NULL).
   b. Deben tener obligatoriamente el mismo nombre que la clave primaria a la que referencian.
   c. Sus valores deben coincidir con un valor de la clave primaria referenciada o ser nulos (si la columna lo permite).
   d. Solo se pueden definir en tablas que no tengan clave primaria.

**8. Si una tabla se encuentra en 1FN (Primera Forma Normal) y tiene una clave primaria compuesta, ¿qué condición específica debemos comprobar para asegurar que cumple la 2FN?**
   a. Que no existan dependencias transitivas.
   b. Que todos los atributos no clave dependan funcionalmente de la clave primaria completa, y no de una parte de ella (dependencia funcional completa).
   c. Que no haya atributos multivaluados.
   d. Que todas las claves candidatas sean simples.

**9. ¿Qué define la Forma Normal de Boyce-Codd (FNBC) que la hace más estricta que la 3FN?**
   a. Ningún atributo, sea clave o no, puede depender de algo que no sea una clave candidata (superclave).
   b. Elimina los grupos repetitivos.
   c. Requiere que no existan valores nulos en ninguna columna.
   d. Se aplica solo cuando hay claves ajenas compuestas.

**10. En la transformación al modelo relacional, si tenemos una Entidad Débil por Identificación dependiente de una Entidad Fuerte, ¿cómo se forma la Clave Primaria (PK) de la tabla débil resultante?**
   a. Se crea un campo autonumérico nuevo como PK.
   b. La PK es únicamente la clave ajena de la entidad fuerte.
   c. La PK es compuesta: la combinación de la PK de la fuerte (como FK) más el atributo discriminante de la débil.
   d. La entidad débil no tiene PK en el modelo físico.

**11. Al transformar una relación 1:N donde la entidad del lado "1" tiene una cardinalidad mínima de 0 (participación opcional), ¿cómo afecta esto a la Clave Ajena (FK) en la tabla resultante?**
   a. La FK debe definirse como `NOT NULL`.
   b. La FK debe admitir valores `NULL`.
   c. Se debe crear una tabla intermedia obligatoriamente para evitar nulos.
   d. La FK se transforma en una clave alternativa.

**12. En una transformación de Jerarquía (EER) usando la solución de "Una tabla para cada entidad" (Superclase y Subclases), ¿qué característica tiene la PK de las tablas de las subclases?**
   a. Tienen su propio ID autoincremental independiente del padre.
   b. Su PK es al mismo tiempo una FK que referencia a la PK de la tabla de la superclase.
   c. No tienen PK, usan la del padre directamente.
   d. La PK se forma concatenando el tipo de subclase con el ID.

**13. En SQL (DDL), si queremos cambiar el nombre de una columna y a la vez su tipo de dato en una sola instrucción, ¿qué cláusula de `ALTER TABLE` debemos usar?**
   a. `MODIFY`
   b. `RENAME COLUMN`
   c. `CHANGE`
   d. `UPDATE`

**14. ¿Cuál es la diferencia funcional principal entre `DATETIME` y `TIMESTAMP` en MySQL según los apuntes?**
   a. `TIMESTAMP` permite fechas anteriores a 1970.
   b. `DATETIME` ocupa menos espacio.
   c. `TIMESTAMP` convierte la hora a UTC para el almacenamiento y se adapta a la zona horaria al recuperarla, además de tener un rango hasta 2038.
   d. `DATETIME` permite actualización automática `ON UPDATE`, pero `TIMESTAMP` no.

**15. ¿Qué sucede si intentamos añadir una restricción `CHECK` a una tabla que ya contiene datos que violan esa restricción en MySQL?**
   a. MySQL corrige los datos automáticamente.
   b. MySQL ignora los datos antiguos y solo valida los nuevos.
   c. La restricción no se aplica a menos que usemos `FORCE`.
   d. MySQL no valida los datos existentes al añadir un `CHECK` (a diferencia de lo que ocurre con FK o PK donde sí daría error).

**16. En la transformación de una relación reflexiva 1:N (ej: Empleado es jefe de otros Empleados), ¿qué estructura se genera?**
   a. Una nueva tabla "Jefes".
   b. Una columna adicional en la tabla `EMPLEADO` que actúa como FK referenciando a la propia tabla `EMPLEADO`.
   c. Una tabla intermedia `EMPLEADO_JEFE` con dos claves foráneas.
   d. No se puede representar, se necesita una agregación.

**17. ¿Qué indica el símbolo de un doble rombo en un diagrama ER?**
   a. Una relación débil (de identificación).
   b. Una relación N:M.
   c. Una relación recursiva.
   d. Una agregación.

**18. En el contexto de normalización, si tenemos `DNI -> Nombre` y `DNI -> Provincia`, y además `CodigoPostal -> Provincia`. ¿Qué tipo de dependencia existe entre `DNI` y `Provincia` si asumimos que `DNI` determina `CodigoPostal`?**
   a. Dependencia Parcial.
   b. Dependencia Transitiva.
   c. Dependencia Multivaluada.
   d. Dependencia Completa.

**19. ¿Cuál es el comportamiento de la restricción `ON UPDATE CASCADE` en una clave foránea?**
   a. Si se modifica la PK del padre, se borran los hijos.
   b. Si se modifica la PK del padre, se actualiza automáticamente el valor de la FK en los hijos.
   c. Impide la modificación de la PK del padre si tiene hijos.
   d. Pone a NULL la FK de los hijos.

**20. ¿Qué tipo de dato usarías preferentemente para una clave primaria autoincremental que nunca será negativa, aprovechando al máximo su rango?**
   a. `INT SIGNED`
   b. `INT UNSIGNED`
   c. `FLOAT`
   d. `DECIMAL`

---

## Parte II: Selección Múltiple (Varias respuestas correctas)

**21. ¿Cuáles de las siguientes afirmaciones sobre la transformación de relaciones 1:1 son VERDADERAS según los apuntes?**
   a. Si la participación es (1,1)-(1,1), se puede propagar la clave a cualquiera de las dos tablas.
   b. La clave ajena propagada en una relación 1:1 debe tener siempre la restricción `UNIQUE`.
   c. Siempre se genera una tercera tabla intermedia, independientemente de la participación.
   d. Si la participación es (1,1)-(0,1), se recomienda llevar la FK a la tabla del lado (0,1) para poder hacerla `NOT NULL`.

**22. ¿Qué elementos definen una restricción de integridad referencial en DDL?**
   a. La columna local (Foreign Key).
   b. La tabla y columna referenciada (Parent Key).
   c. Las acciones de disparo (`ON DELETE`, `ON UPDATE`).
   d. El tipo de dato `BLOB`.

**23. Selecciona qué afirmaciones son correctas respecto a los atributos en el modelo ER.**
   a. Un atributo identificador nunca puede ser compuesto.
   b. Los atributos derivados se representan con una línea punteada.
   c. Los atributos multivaluados se transforman en una nueva tabla en el modelo relacional.
   d. Un atributo compuesto (ej: Dirección) se transforma en el modelo relacional concatenando sus valores en una sola columna.

**24. ¿Cuáles de las siguientes son ventajas de usar Vistas (`VIEWS`) en el diseño físico?**
   a. Aumentan la velocidad de escritura de datos.
   b. Simplifican consultas complejas para el usuario.
   c. Proporcionan una capa de seguridad restringiendo el acceso a columnas específicas.
   d. Almacenan físicamente una copia de los datos para backup.

**25. Para normalizar una base de datos a 3FN, ¿qué pasos previos son obligatorios?**
   a. La tabla debe estar ya en 1FN (valores atómicos).
   b. La tabla debe estar ya en 2FN (eliminación de dependencias parciales).
   c. Deben haberse creado índices `UNIQUE` para todas las columnas.
   d. Deben haberse eliminado las dependencias transitivas.


