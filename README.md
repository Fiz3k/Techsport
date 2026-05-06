# Techsport
Diagrama de Arquitectura del sitio
1. Flujo seguro desde el cliente hasta la base de datos
El diagrama muestra una comunicación cifrada mediante HTTPS entre el navegador del cliente y el backend de TechStore. Los datos sensibles de pago (como números de tarjeta) nunca llegan directamente a la base de datos, sino que se tokenizan a través de una pasarela de pagos externa (Stripe, MercadoPago, etc.). Esto evita que información confidencial sea almacenada localmente, reduciendo el riesgo de filtraciones.

2. Backend como capa de validación y protección
El backend no solo procesa solicitudes, sino que aplica dos medidas de seguridad críticas antes de tocar la base de datos:

Validaciones de entrada: verifica que los montos sean positivos, que los IDs existan, que el stock sea suficiente, etc.

Consultas parametrizadas (Prepared Statements): elimina por completo el riesgo de inyección SQL al separar los datos de las instrucciones SQL.

3. Base de datos SQL con tres niveles de instrucciones
El diagrama identifica explícitamente los tres tipos de instrucciones SQL necesarias:

DDL (CREATE TABLE, ALTER, etc.) → para definir la estructura inicial de usuarios, productos, transacciones y sus relaciones.

DML (INSERT, SELECT, UPDATE) → para operaciones diarias como registrar compras, consultar stock y actualizar estados de pago.

DCL (GRANT, REVOKE) → para asignar roles específicos (ej. pagos, reportes) y limitar permisos según el principio de mínimo privilegio.

4. Validación de transacciones con ACID
El diagrama refleja que cada operación de pago se envuelve en una transacción SQL explícita (BEGIN...COMMIT / ROLLBACK). Esto garantiza:

Atomicidad: si falla la pasarela de pagos, no se descuenta stock ni se confirma la orden.

Consistencia: el inventario y el estado de la transacción siempre quedan en un estado válido.

Aislamiento: dos compras simultáneas no interfieren entre sí.

Durabilidad: una vez confirmado el pago, los datos persisten incluso ante caídas del sistema.
