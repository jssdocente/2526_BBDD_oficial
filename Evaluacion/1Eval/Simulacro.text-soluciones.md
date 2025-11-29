### 🔑 1Evaluación-Simulacro: Hoja de Soluciones

#### Parte I: Selección Única
1.  **b** (La transacción garantiza atomicidad de un conjunto de operaciones).
2.  **c** (Línea punteada en óvalo indica atributo derivado).
3.  **b** (0 es el mínimo -opcional-, 1 es el máximo).
4.  **c** (Disjunta significa que no hay solapamiento entre subclases).
5.  **b** (Permite abstraer una relación como si fuera una entidad para relacionarla de nuevo).
6.  **b** (Es una clave candidata que no fue elegida como primaria, por tanto, alternativa).
7.  **c** (Es la definición de integridad referencial; permite nulos a menos que sea NOT NULL).
8.  **b** (La 2FN elimina dependencias parciales, cruciales en claves compuestas).
9.  **a** (Es más estricta con las dependencias funcionales en claves compuestas solapadas).
10. **c** (PK compuesta por la FK del padre + discriminante propio).
11. **b** (Al ser opcional (0), puede que no tenga relación, por lo que el campo FK debe permitir NULL).
12. **b** (La PK de la subclase es igual a la del padre y actúa como FK hacia él).
13. **c** (`CHANGE` permite renombrar y cambiar tipo; `MODIFY` solo cambia tipo; `RENAME` solo nombre).
14. **c** (`TIMESTAMP` trabaja con UTC y tiene rango hasta 2038; `DATETIME` es literal).
15. **b** (MySQL no valida datos existentes para `CHECK`, solo nuevos).
16. **b** (Es una FK recursiva en la misma tabla).
17. **a** (El doble rombo indica relación débil/identificación).
18. **b** (DNI -> CP -> Provincia, es una transitividad).
19. **b** (Propaga el cambio del valor de la clave).
20. **b** (`UNSIGNED` elimina los negativos, doblando el rango positivo disponible).

#### Parte II: Selección Múltiple
21. **a, b, d** (La c es falsa, casi nunca generan tabla nueva).
22. **a, b, c** (Son los componentes de `FOREIGN KEY ... REFERENCES ... ON ...`).
23. **b, c** (La 'a' es falsa, pueden ser compuestos; la 'd' es falsa, se separan en columnas).
24. **b, c** (Las vistas son virtuales, no almacenan datos ni mejoran escritura).
25. **a, b, d** (Son los requisitos acumulativos de la normalización).