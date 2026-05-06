# Techsport
Diagrama de Arquitectura del sitio
1. Flujo seguro desde el cliente hasta la base de datos
El diagrama muestra una comunicación cifrada mediante HTTPS entre el navegador del cliente y el backend de TechStore. Los datos sensibles de pago (como números de tarjeta) nunca llegan directamente a la base de datos, sino que se tokenizan a través de una pasarela de pagos externa (Stripe, MercadoPago, etc.). Esto evita que información confidencial sea almacenada localmente, reduciendo el riesgo de filtraciones.

2. Backend como capa de validación y protección
El backend no solo procesa solicitudes, sino que aplica dos medidas de seguridad críticas antes de tocar la base de datos:

Validaciones de entrada: verifica que los montos sean positivos, que los IDs existan, que el stock sea suficiente, etc.

Consultas parametrizadas (Prepared Statements): elimina por completo el riesgo de inyección SQL al separar los datos de las instrucciones SQL.

