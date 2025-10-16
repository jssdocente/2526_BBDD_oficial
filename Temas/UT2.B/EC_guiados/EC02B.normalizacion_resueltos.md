# 📚 UT2.B Ejercicios de normalización resueltos

### **Ejercicio 1: El Registro de la Biblioteca (Hasta 1FN)**

**Objetivo:** Entender el requisito más fundamental de una base de datos relacional: la atomicidad de los datos.

*   **Enunciado:**
    La biblioteca del barrio utiliza una simple hoja de cálculo para registrar los préstamos. La tabla inicial es la siguiente:

    **Tabla: `PRESTAMOS_BIBLIOTECA`**

    | ID_Prestamo | NIF_Usuario | Nombre_Usuario | Libros_Prestados (ISBN y Título) | Fecha_Prestamo |
    | :--- | :--- | :--- | :--- | :--- |
    | 101 | 12345678A | Ana Sanz | '978-1, Don Quijote', '978-2, La Sombra del Viento'| 2025-10-15 |
    | 102 | 87654321B | Luis Prado | '978-3, Cien Años de Soledad' | 2025-10-16 |
    | 103 | 12345678A | Ana Sanz | '978-1, Don Quijote' | 2025-10-20 |

#### **Análisis y Solución (Paso a 1FN)**

*   **Definición de 1FN (Primera Forma Normal):** Una tabla está en 1FN si todos sus atributos contienen valores **atómicos** (indivisibles) y no existen grupos repetitivos en una misma fila.

*   **Identificación del Problema:**
    La columna `Libros_Prestados` viola claramente la 1FN. En la fila con `ID_Prestamo` 101, tenemos dos libros distintos en la misma celda. Esto es un **atributo multivaluado**. Si quisiéramos buscar qué usuario tiene "Don Quijote", tendríamos que buscar dentro de una cadena de texto, lo cual es terriblemente ineficiente y propenso a errores.

*   **Solución:**
    Para resolverlo, debemos asegurar que cada fila y cada columna contengan un único valor. La forma correcta es crear una fila separada para cada libro prestado.

    **Tabla: `PRESTAMOS_BIBLIOTECA` en 1FN**

    | ID_Prestamo | NIF_Usuario | Nombre_Usuario | ISBN_Libro | Titulo_Libro | Fecha_Prestamo |
    | :--- | :--- | :--- | :--- | :--- | :--- |
    | 101 | 12345678A | Ana Sanz | 978-1 | Don Quijote | 2025-10-15 |
    | 101 | 12345678A | Ana Sanz | 978-2 | La Sombra del Viento| 2025-10-15 |
    | 102 | 87654321B | Luis Prado | 978-3 | Cien Años de Soledad| 2025-10-16 |
    | 103 | 12345678A | Ana Sanz | 978-1 | Don Quijote | 2025-10-20 |


**Conclusión:** ¡Y listo! El ejercicio termina aquí. Hemos transformado una tabla no relacional en una que cumple la 1FN. Ahora podríamos definir una clave primaria compuesta, por ejemplo `{ID_Prestamo, ISBN_Libro}`.

---

### **Ejercicio 2: Gestión de Pedidos (De 1FN a 2FN y 3FN)**

**Objetivo:** Identificar y eliminar dependencias parciales y transitivas.

*   **Enunciado:**
    Una pequeña tienda online utiliza la siguiente tabla (ya en 1FN) para gestionar los detalles de sus pedidos.

    **Tabla: `DETALLE_PEDIDO` (en 1FN)**
    **Clave Primaria (CP):** `{ID_Pedido, ID_Producto}`

    | ID_Pedido| ID_Producto| Nombre_Producto| Cantidad | Precio_Unitario | ID_Cliente | Nombre_Cliente | Direccion_Cliente |
    | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
    | P1001 | A01 | Teclado USB | 1 | 25.50 | C01 | Juan Pérez | Calle Mayor, 1 |
    | P1001 | B02 | Ratón Inalámbrico| 1 | 15.00 | C01 | Juan Pérez | Calle Mayor, 1 |
    | P1002 | A01 | Teclado USB | 2 | 25.50 | C02 | Ana Solís | Av. del Parque, 2|
    | P1003 | C03 | Monitor 24" | 1 | 150.00 | C01 | Juan Pérez | Calle Mayor, 1 |

#### **Análisis y Solución (Paso a 2FN y 3FN)**

- **Paso 1: Hacia 2FN (Eliminar Dependencias Parciales)**

    *   **Definición de 2FN:** Una tabla está en 2FN si está en 1FN y todos sus atributos no clave dependen de forma **completa** de la clave primaria.
    *   **Identificación del Problema:**
        *   `Cantidad`: Depende de `{ID_Pedido, ID_Producto}`. Para saber la cantidad, necesito saber de qué pedido Y de qué producto hablamos. **Dependencia Completa - OK.**
        *   `Nombre_Producto`, `Precio_Unitario`: Dependen solo de `ID_Producto`. No necesito el `ID_Pedido` para saber el nombre o el precio de un producto. **Dependencia Parcial - PROBLEMA.**
        *   `ID_Cliente`, `Nombre_Cliente`, `Direccion_Cliente`: Dependen solo de `ID_Pedido`. Todos los productos de un mismo pedido tienen el mismo cliente. **Dependencia Parcial - PROBLEMA.**
    *   **Solución:** Creamos tablas separadas para las dependencias parciales.

    **Tabla 1: `PEDIDO_PRODUCTO` (en 2FN)**
    **CP:** `{ID_Pedido, ID_Producto}`

    | ID_Pedido| ID_Producto| Cantidad |
    | :--- | :--- | :--- |
    | P1001 | A01 | 1 |
    | P1001 | B02 | 1 |
    | P1002 | A01 | 2 |
    | P1003 | C03 | 1 |

    **Tabla 2: `PRODUCTOS` (en 2FN)**
    **CP:** `{ID_Producto}`

    | ID_Producto| Nombre_Producto | Precio_Unitario |
    | :--- | :--- | :--- |
    | A01 | Teclado USB | 25.50 |
    | B02 | Ratón Inalámbrico| 15.00 |
    | C03 | Monitor 24" | 150.00 |

    **Tabla 3: `PEDIDOS` (en 2FN)**
    **CP:** `{ID_Pedido}`

    | ID_Pedido| ID_Cliente | Nombre_Cliente | Direccion_Cliente |
    | :--- | :--- | :--- | :--- |
    | P1001 | C01 | Juan Pérez | Calle Mayor, 1 |
    | P1002 | C02 | Ana Solís | Av. del Parque, 2 |
    | P1003 | C01 | Juan Pérez | Calle Mayor, 1 |

-   **Paso 2: Hacia 3FN (Eliminar Dependencias Transitivas)**
    *   **Definición de 3FN:** Una tabla está en 3FN si está en 2FN y no existen dependencias transitivas (un atributo no clave no puede depender de otro atributo no clave).
    *   **Identificación del Problema:**
        *   Revisamos las tablas resultantes: `PEDIDO_PRODUCTO` y `PRODUCTOS` ya están en 3FN.
        *   En la tabla `PEDIDOS`, tenemos la siguiente cadena: `ID_Pedido` (CP) -> `ID_Cliente` (no clave) -> `Nombre_Cliente`, `Direccion_Cliente` (no clave). `Nombre_Cliente` y `Direccion_Cliente` dependen de `ID_Cliente`, que no es la clave primaria. **Dependencia Transitiva - PROBLEMA.**
    *   **Solución:** Separamos la información del cliente en su propia tabla.

    **Tabla 3.1: `PEDIDOS_FINAL` (en 3FN)**
    **CP:** `{ID_Pedido}`

    | ID_Pedido| ID_Cliente (FK) |
    | :--- | :--- |
    | P1001 | C01 |
    | P1002 | C02 |
    | P1003 | C01 |

    **Tabla 4: `CLIENTES` (en 3FN)**
    **CP:** `{ID_Cliente}`

    | ID_Cliente | Nombre_Cliente | Direccion_Cliente |
    | :--- | :--- | :--- |
    | C01 | Juan Pérez | Calle Mayor, 1 |
    | C02 | Ana Solís | Av. del Parque, 2 |


**Conclusión:** Hemos descompuesto la tabla original en 4 tablas (`PEDIDO_PRODUCTO`, `PRODUCTOS`, `PEDIDOS_FINAL`, `CLIENTES`), cada una representando un único concepto y todas en 3FN.

---

### **Ejercicio 3: Asignación de Tutores (De 2FN a 3FN y FNBC)**

**Objetivo:** Entender la Forma Normal de Boyce-Codd (FNBC), que es una versión más estricta de la 3FN.

*   **Enunciado:**
    En una academia, se asignan tutores a los alumnos para asignaturas específicas. La tabla está en 2FN. Se aplican las siguientes reglas de negocio:
    1.  Un alumno solo puede tener un tutor por asignatura.
    2.  Cada tutor está especializado y enseña una única asignatura.
    3.  Una asignatura puede ser enseñada por varios tutores.

    **Tabla: `TUTORIAS` (en 2FN)**
    **Claves Candidatas:** `{ID_Alumno, ID_Asignatura}` y `{ID_Alumno, ID_Tutor}`. Elegimos la primera como **CP**.

    | ID_Alumno| ID_Asignatura| ID_Tutor | Nombre_Tutor |
    | :--- | :--- | :--- | :--- |
    | A01 | MATE | T05 | Carlos Ruiz |
    | A01 | FISI | T08 | Laura Gil |
    | A02 | MATE | T06 | Ana Vega |
    | A03 | FISI | T08 | Laura Gil |

#### **Análisis y Solución (Paso a 3FN y FNBC)**

*   **Paso 1: Hacia 3FN**
    *   **Análisis de dependencias transitivas:**
        *   CP -> `ID_Tutor`.
        *   `ID_Tutor` -> `Nombre_Tutor`.
        *   Tenemos una dependencia transitiva: `CP -> ID_Tutor -> Nombre_Tutor`.
    *   **Solución:** Descomponemos para eliminarla.

    **Tabla 1: `ASIGNACION_TUTORIA` (en 3FN)**
    **CP:** `{ID_Alumno, ID_Asignatura}`

    | ID_Alumno| ID_Asignatura| ID_Tutor (FK) |
    | :--- | :--- | :--- |
    | A01 | MATE | T05 |
    | A01 | FISI | T08 |
    | A02 | MATE | T06 |
    | A03 | FISI | T08 |

    **Tabla 2: `TUTORES` (en 3FN)**
    **CP:** `{ID_Tutor}`

    | ID_Tutor | Nombre_Tutor |
    | :--- | :--- |
    | T05 | Carlos Ruiz |
    | T08 | Laura Gil |
    | T06 | Ana Vega |

*   **Paso 2: Hacia FNBC (Forma Normal de Boyce-Codd)**
    
    *   **Definición de FNBC:** Una tabla está en FNBC si para cada dependencia funcional no trivial $X \rightarrow Y$, $X$ es una **superclave** (es decir, una clave candidata o un superconjunto de una).
    *   **Identificación del Problema:**
        *   Revisemos las tablas. `TUTORES` está en FNBC.
        *   Ahora miremos `ASIGNACION_TUTORIA` y recordemos la regla de negocio 2: "Cada tutor enseña una única asignatura". Esto implica la dependencia funcional: `ID_Tutor -> ID_Asignatura`.
        *   Analicemos esta dependencia: `ID_Tutor` (el determinante) **NO es una superclave** de la tabla `ASIGNACION_TUTORIA` (la clave es `{ID_Alumno, ID_Asignatura}`).
        *   Por lo tanto, la tabla viola la FNBC.
    *   **Solución:** Debemos descomponer la tabla `ASIGNACION_TUTORIA` para que cada determinante sea una superclave.

    **Tabla 1.1: `ALUMNO_TUTOR` (en FNBC)**
    **CP:** `{ID_Alumno, ID_Tutor}`

    | ID_Alumno| ID_Tutor (FK) |
    | :--- | :--- |
    | A01 | T05 |
    | A01 | T08 |
    | A02 | T06 |
    | A03 | T08 |

    **Tabla 1.2: `TUTOR_ASIGNATURA` (en FNBC)**
    **CP:** `{ID_Tutor}`

    | ID_Tutor (FK)| ID_Asignatura |
    | :--- | :--- |
    | T05 | MATE |
    | T08 | FISI |
    | T06 | MATE |

**Conclusión:** La FNBC nos ha forzado a una descomposición más fina para reflejar con mayor precisión las reglas de negocio y evitar anomalías. Ahora tenemos 3 tablas en FNBC.

---

### **Ejercicio 4: El Gran Caso (Aplicando Todo)**

**Objetivo:** Enfrentarse a un problema complejo desde el inicio, aplicando todas las formas normales en secuencia.

*   **Enunciado:**
    Una empresa de RRHH tiene una tabla "todo en uno" para registrar la asignación de sus consultores a los proyectos de sus clientes.

    **Tabla: `REGISTRO_PROYECTOS` (No está en 1FN)**
    **Intención de Clave Primaria:** `{ID_Proyecto, ID_Consultor}`

    | ID_Proyecto| Nombre_Proyecto| ID_Cliente | Nombre_Cliente | ID_Consultor| Nombre_Consultor| Habilidades_Consultor | Horas_Asignadas | ID_Manager_Proyecto| Nombre_Manager |
    | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
    | P01 | Web Corporativa| C01 | ACME S.L. | E101 | Ana Sanz | 'Java, SQL, Git', 'PHP'| 120 | M5 | Carlos Ruiz |
    | P01 | Web Corporativa| C01 | ACME S.L. | E102 | Luis Prado | 'HTML, CSS, JS' | 100 | M5 | Carlos Ruiz |
    | P02 | App Móvil | C02 | GIGA Corp. | E101 | Ana Sanz | 'Java, SQL, Git', 'PHP'| 150 | M6 | Eva Costa |

#### **Análisis y Solución Completa**

*   **Paso 1: Hacia 1FN**
    *   **Problema:** La columna `Habilidades_Consultor` es multivaluada.
    *   **Solución:** Creamos una tabla separada para las habilidades.

    **Tabla A: `PROYECTO_CONSULTOR` (en 1FN)**
    **CP:** `{ID_Proyecto, ID_Consultor}`

    | ID_Proyecto| Nombre_Proyecto| ID_Cliente | Nombre_Cliente | ID_Consultor| Nombre_Consultor| Horas_Asignadas| ID_Manager_Proyecto| Nombre_Manager |
    | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
    | P01 | Web Corporativa| C01 | ACME S.L. | E101 | Ana Sanz | 120 | M5 | Carlos Ruiz |
    | P01 | Web Corporativa| C01 | ACME S.L. | E102 | Luis Prado | 100 | M5 | Carlos Ruiz |
    | P02 | App Móvil | C02 | GIGA Corp. | E101 | Ana Sanz | 150 | M6 | Eva Costa |

    **Tabla B: `HABILIDADES_CONSULTOR` (en 1FN)**
    **CP:** `{ID_Consultor, Habilidad}`

    | ID_Consultor | Habilidad |
    | :--- | :--- |
    | E101 | Java |
    | E101 | SQL |
    | E101 | Git |
    | E101 | PHP |
    | E102 | HTML |
    | E102 | CSS |
    | E102 | JS |

*   **Paso 2: Hacia 2FN (sobre la Tabla A)**
  
    *   **CP:** `{ID_Proyecto, ID_Consultor}`
    *   **Dependencias Parciales:**
        *   `Nombre_Proyecto`, `ID_Cliente`, `Nombre_Cliente`, `ID_Manager_Proyecto`, `Nombre_Manager` dependen solo de `ID_Proyecto`.
        *   `Nombre_Consultor` depende solo de `ID_Consultor`.
    *   **Dependencia Completa:** `Horas_Asignadas`.
    *   **Solución:** Descomponemos `PROYECTO_CONSULTOR`.

    **Tabla A1: `ASIGNACIONES` (2FN)** - CP: `{ID_Proyecto, ID_Consultor}`
    `{ID_Proyecto, ID_Consultor, Horas_Asignadas}`

    **Tabla A2: `PROYECTOS` (2FN)** - CP: `{ID_Proyecto}`
    `{ID_Proyecto, Nombre_Proyecto, ID_Cliente, Nombre_Cliente, ID_Manager_Proyecto, Nombre_Manager}`

    **Tabla A3: `CONSULTORES` (2FN)** - CP: `{ID_Consultor}`
    `{ID_Consultor, Nombre_Consultor}`

*   **Paso 3: Hacia 3FN (Revisando A1, A2, A3 y B)**
    *   A1, A3 y B ya están en 3FN.
    *   **Problema en la tabla `PROYECTOS` (A2):**
        *   `ID_Proyecto` -> `ID_Cliente` -> `Nombre_Cliente`. **Transitiva.**
        *   `ID_Proyecto` -> `ID_Manager_Proyecto` -> `Nombre_Manager`. **Transitiva.**
    *   **Solución:** Descomponemos `PROYECTOS`.

    **Tabla A2.1: `PROYECTOS_FINAL` (3FN)** - CP: `{ID_Proyecto}`
    `{ID_Proyecto, Nombre_Proyecto, ID_Cliente (FK), ID_Manager_Proyecto (FK)}`

    **Tabla C: `CLIENTES` (3FN)** - CP: `{ID_Cliente}`
    `{ID_Cliente, Nombre_Cliente}`

    **Tabla D: `MANAGERS` (3FN)** - CP: `{ID_Manager_Proyecto}`
    `{ID_Manager_Proyecto, Nombre_Manager}`

*   **Paso 4: Hacia FNBC**
    *   Revisando todas las tablas finales, no encontramos dependencias donde un determinante no sea una superclave. Todas las tablas están también en FNBC.

**Conclusión Final del Caso Complejo:**

Hemos transformado una única tabla caótica en un conjunto de 6 tablas normalizadas, limpias y eficientes:
1.  `ASIGNACIONES`
2.  `CONSULTORES`
3.  `HABILIDADES_CONSULTOR`
4.  `PROYECTOS_FINAL`
5.  `CLIENTES`
6.  `MANAGERS`