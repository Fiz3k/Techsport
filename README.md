# Techsport
Diagrama de Arquitectura del sitio
1. Flujo seguro desde el cliente hasta la base de datos
El diagrama muestra una comunicación cifrada mediante HTTPS entre el navegador del cliente y el backend de TechStore. Los datos sensibles de pago (como números de tarjeta) nunca llegan directamente a la base de datos, sino que se tokenizan a través de una pasarela de pagos externa (Stripe, MercadoPago, etc.). Esto evita que información confidencial sea almacenada localmente, reduciendo el riesgo de filtraciones.

