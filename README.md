# proyecto_diplomatura_vinoble
## Descrpcion
app para para automatizar la gestio y control de la produccion, distribucion y venta de vinos

## 🚀 ¿Para qué sirve?
Aplicación para gestionar inventario y ventas de vinos en tiempo real. Registra y controla stock por añada, variedad y otras características. Incluye distribución a clientes (hoteles, restaurantes, vinotecas y particulares) y seguimiento de ventas cobradas y pendientes, mejorando trazabilidad y eficiencia.

## 🍷a quien va dirigido?
Este proyecto está dirigido a entusiastas del mundo del vino de todas las edades que desarrollan pequeños emprendimientos de producción y venta. Ofrece una herramienta simple e intuitiva para gestionar el negocio de forma ordenada, ahorrar tiempo y trabajar con mayor eficiencia, brindando tranquilidad y bienestar para seguir creando vinos fatasticos.

## 🤖que probema resuelve?
Este proyecto resuelve la falta de herramientas simples e integrales para pequeños productores y emprendedores del mundo del vino. Muchas veces no cuentan con una aplicación que les permita gestionar su negocio de forma práctica desde el teléfono. Esta app busca facilitar el control del inventario, la producción y las ventas, haciendo el proceso más ordenado, amigable y eficiente, y brindando una solución accesible para quienes, sin ser grandes productores, necesitan gestionar su emprendimiento con mayor facilidad.

## 🪂Beneficios
Va a permitir a pequeños emprendedores del vino gestionar su negocio de forma simple y ordenada, ahorrando tiempo y reduciendo errores. Facilita el control del stock y las ventas en tiempo real desde el teléfono, mejorando la eficiencia y la toma de decisiones, y brindando mayor tranquilidad en el día a día. 

## 🐦 Tecnologías utilizadas
Excel, Vercel, Canva

## 🎨 Diseño Visual y Prototipo
## Puedes ver el diseño visual completo y las pantallas de la aplicación en el siguiente enlace:
(AQUI_IRIA_EL_LIN_DE_CANCA 

## Segunda Etapa
## 📝 Descripción del Proyecto
El proyecto detalla la especificación funcional y el diseño de arquitectura de datos para una aplicación móvil de uso individual y exclusivo para el vendedor en la calle. El objetivo principal es dotar al comercial de una herramienta ágil en su teléfono celular que resuelva la pérdida de información y los errores de cálculo que ocurren durante la preventa y el reparto diario.

A diferencia de los sistemas corporativos tradicionales, esta solución está diseñada específicamente para operar de manera rápida en movilidad, permitiendo al vendedor consultar su stock real en el momento, registrar las botellas que entrega a cada cliente y controlar de forma rigurosa quién le pagó y quién posee saldos pendientes en cuenta corriente.

## Objetivos e Implementación Funcional en Celular
La aplicación se estructura como un sistema relacional cerrado de gestión personal enfocado en optimizar el día a día del vendedor mediante tres funciones centrales:

1. **Catálogo e Inventario de Bolsillo:** Permite al vendedor saber con precisión qué etiquetas tiene disponibles en su vehículo o depósito antes de confirmar una venta, detallando marcas y tipos de uva.
2. **Administración Autónoma de Clientes:** Centraliza el perfil comercial de los compradores de su zona (restaurantes, vinotecas, clientes particulares) y sus condiciones de pago pactadas.
3. **Control de Reparto y Cobranzas (Libro de Ruta):** Registra cada transacción en tiempo real al momento de dejar las botellas, automatizando el cálculo de deudas y saldos en cuenta corriente sin necesidad de usar planillas de papel.

## 🛠️ 3. Arquitectura del Modelo de Datos (Estructura de Tablas)
Para garantizar el funcionamiento de la aplicación en el dispositivo móvil, el modelo se organiza en tres tablas de datos interconectadas mediante identificadores (IDs):

### 📊 Tabla 1: `Vinos` (Inventario del Vendedor)
Es el catálogo de productos que el vendedor lleva consigo o tiene asignado para ofrecer.
* **ID_Vino (Clave Primaria):** Código numérico único asignado a cada etiqueta para agilizar la carga en la pantalla del celular.
* **Marca_Bodega / Etiqueta_Nombre:** Datos de identificación comercial del vino (Ej. Catena Zapata, Angelica Zapata).
* **Tipo_Uva:** Clasificación enológica (Malbec, Cabernet, Chardonnay, etc.) que permite al vendedor filtrar rápidamente los productos según el interés del cliente.
* **Proveedor:** Distribuidora o bodega de origen que provee el lote.
* **Precio_Costo y Precio_Venta:** Valores base para que la aplicación calcule automáticamente los montos de facturación en la calle.
* **Stock_Actual:** Cantidad de botellas disponibles en tiempo real. Disminuye con cada entrega registrada por el vendedor.

### 👥 Tabla 2: `Clientes` (Agenda Comercial)
Es la base de datos personal de los clientes que componen la ruta de venta del usuario.
* **ID_Cliente (Clave Primaria):** Código identificador único para cada comercio o comprador particular.
* **Nombre_Razon_Social / Telefono:** Información esencial de contacto para llamadas o geolocalización rápida desde el celular.
* **Condicion_Pago:** Define la regla de cobro para ese cliente ("Efectivo/Inmediato" o autorizado a operar en "Cuenta Corriente").
* **Limite_Credito:** Monto máximo de deuda que el vendedor le permite acumular a ese cliente antes de suspenderle las entregas en cuenta corriente.

### 💸 Tabla 3: `Movimientos` (Registro de Transacciones en Campo)
Actúa como el libro diario donde el vendedor anota cada acción que sucede durante su jornada en la calle (entregas de mercadería o cobros de dinero).
* **ID_Movimiento (Clave Primaria):** Número correlativo interno que genera la App por cada operación.
* **Fecha:** Registro temporal automático de cuándo se realizó la visita o el cobro.
* **ID_Cliente / ID_Vino (Claves Foráneas):** Vinculación directa que indica a qué cliente se visitó y qué producto se le entregó.
* **Cantidad_Botellas:** Volumen físico entregado en el momento (resta del stock del vendedor).
* **Total_Transaccion:** Expresión financiera de la operación. Se registra con signo **positivo** cuando se entregan vinos (aumenta la deuda del cliente) y con signo **negativo** cuando el cliente realiza un pago (ingreso de dinero que reduce la deuda).
* **Estado_Pago:** Clasificación de la transacción en el momento de la carga ("En Cuenta Corriente", "Pagado", "Abono a Deuda").

## 💻 4. Procedimiento Operativo de la App (Lógica de Negocio en Movilidad)

### Flujo A: Registro de Venta y Descuento de Stock en la Calle
Cuando el vendedor visita un cliente y le deja mercadería:
1. El vendedor abre la App en su celular, selecciona el cliente e ingresa el `ID_Vino` y la `Cantidad_Botellas` entregadas.
2. La aplicación da de alta la transacción en la tabla `Movimientos`.
3. Internamente, la App actualiza la tabla `Vinos` restando las unidades vendidas (`Stock_Actual = Stock_Actual - Cantidad_Botellas`), permitiendo al vendedor saber exactamente cuántas botellas le quedan en el vehículo para el próximo cliente.

### Flujo B: Consulta de Cuenta Corriente y Cobranzas en Tiempo Real
Cuando un cliente solicita dejar el pedido en cuenta corriente o realiza un pago parcial de su deuda:
1. El vendedor busca al cliente en su aplicación.
2. La App escanea la tabla `Movimientos` filtrando por el `ID_Cliente` y realiza una suma algebraica de la columna `Total_Transaccion`.
3. **Acción de Alerta:** Si el cliente solicita mercadería en cuenta corriente y el saldo acumulado supera su `Limite_Credito`, la aplicación del celular muestra una advertencia en pantalla, indicando al vendedor que debe exigir un pago antes de bajar más botellas.
4. **Registro de Cobro:** Si el cliente paga, el vendedor registra un movimiento de tipo "Abono a Deuda" con valor negativo, actualizando el saldo deudor de forma inmediata.

## santiagos-app-ph9g
