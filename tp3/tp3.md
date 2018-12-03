# Trabajo práctico 3

## Mejorar el sistema de pago existente

#### Cliente

Hoteles Pepito, una empresa lider en el mercado hotelero con 45 años de experiencia en la region latinoamericana.
Con más de 120 hoteles en las mejores ubicaciones de 6 países (Argentina, Brasil, Uruguay, Chile, Venezuela, Mexico), en Hoteles Pepito ofrecemos experiencias vacacionales de alta calidad, avaladas por la satisfacción de nuestros clientes.

Servicios indpendientes:
* Hospedaje
* Gimnasio
* Pileta
* Jacuzzi
* Bar
* Salon de Juegos
* Heladera
* Caja Fuerte
* Sauna
* Spa
* Restaurante

Los Paquetes hoteleros pueden ser armados utilizando un subconjunto del total, no hay paquetes prearmados, dejando al cliente la satisfaccion de armar su estadía de forma autónoma. Es importante aclarar que como Hoteles Pepito es una franquicia las tarifas de base deben mantenerse en todos los países sumando los impuestos que haya que respetar en cada país según sus normas.

### Contexto

En el pasado semestre, particularmente durante la epoca de invierno, el equipo de marketing y logistica tuvieron el encargo de realizar encuestas a razon de adquirir, y analizar los diferentes comportamientos de los clientes. Dichas encuestas revelaron que los usuarios no confían en los sistemas de pagos que ofrecen los hoteles, y las razones son bastante variadas. Algunos de los ejemplos obtenidos son sistemas deficientes, sistemas con respuesta que tardan demasiado tiempo, etc. Por otro lado, uno de los servicios habituales que nuestra gama de hoteles suele manejar es la venta inmediata y/o diferida de paquetes hotelero,

Tabla de Tarifas Actual
|Servicio de hospedaje básico|Bar   |Jacuzzi|Heladera|Pileta Climatizada|Gimnasio
|:----:|:----:|:-----:|:---:|:---:|:---:|:---:
|300 u$s|10 u$s |35 u$s  |10 u$s|25 u$s|27 u$s

Paquetes
|Servicio de hospedaje básico|Bar   |Jacuzzi|Heladera|Pileta Climatizada|Gimnasio|Total
|:----:|:----:|:-----:|:---:|:---:|:---:|:---:|:---:
|X|X|O|X|O|O|275 u$s
|X|X|O|X|O|X|300 u$s
|X|X|O|X|X|X|325 u$s
|X|X|X|X|X|X|350 u$s

los cuales en un promedio elevado, los clientes aprovechan y obtienen de todas formas sin pagarlos (informacion vital que pudo obtenerse gracias al registro y rastreo de los mismos).

Es de publico conocimiento que los avances tecnologicos actuales pueden beneficiar a la empresa de diferetes maneras. Nuestro principal objetivo a mediano/largo plazo es tener un mejor monitoreo de como se maneja el cobro independiemente de la ubicación geográfica de los hoteles, así como también poder inferir comportamientos comunes de nuestros clientes.

Por este motivo la empresa Hoteles Pepito S.R.L., requiere realizar un sistema que permita centralizar los metodos de pago, de forma tal que los clientes puedan confiar en que no les van a cobrar algo que no utilizaron además de que los hoteles también puedan confiar en que la gente no se salteará ningún servicio utilizado. Esto se debe mayormente al sistema actual de cobro hacia el cliente. Este se ha manifestado disconforme, de manera incremental, ante los cuadros tarifarios alegando no haber utilizados ciertos servicios, intentando asi, lograr un escape al pago.

### Alcance

El alcance, será el de integrar en cada uno de los hoteles los dispositivos que permitiran acercar una tarjeta magnética para habilitarlos (i.e para abrir el bar, etc). De esta forma se sabrá cuales fueron los servicios utilizados para la hora del cobro.

Por otro lado, también habrá que hacer un sistema que pueda leer los datos de la tarjeta magnética para luego comunicarse con los sistemas de cobro existentes (e.g visa, mastercard, etc) para realizar finalmente el cobro.

Finalmente, vemos una oportunidad de negocio en tratar los datos de los usuarios (i.e qué servicios usan y cuales no), por lo que esto también será parte del alcance.


Sera parte del alcance del sistema los siguientes puntos:

* Contar con una interfaz que permita integrarlo en otros sitemas ya existentes
* Permitirle a los usuarios utilizar tarjetas magneticas/NFC para acceder a los distintos servicios del hotel
* Facilitar el cobro de los gastos del usuario llevando un registro de los mismos
  * Llevar un registro de los gastos con dichas tarjetas
  * Llevar un registro más detallado de los gastos de los usuarios en una base de datos del hotel
* Permitirle a los administradores del hotel acceder a los datos de gastos de los usuarios
* Permitirle a los administradores acceder a graficos de uso y analytics

No es parte del alcance del sistema los siguietes puntos:

* Implementar un subsistema de facturación
* Implementar un sistema de reservas y gestion hotelera

### Especificaciones

#### Requerimiento 1

Al ser un plugin de sistemas de gestion hotelera, se requiere que la entrada al sistema sea una API que exponemos al sistema externo, que recibe un usuario y un ID de tarjeta, para avisarnos que X usuario tiene Y tarjeta en este momento.

##### Especificación

El sistema externo enviará los datos necesarios a la API, ésta debe recibir los datos y validar que sean los necesarios, es decir, que contenga información de usuario y tarjeta.
Luego de la validación debe guardar los datos en la base de datos, y enviar una respuesta de confirmación de recepción.
En caso de algun error se debe responder con el status code HTTP que corresponda.

Se adjuntara un diagrama de flujo para clarificar el proceso.

Consideraciones:
* La API debe ser RESTful
* Se debe guardar la información enviada por el sistema externo en una base de datos (MongoDB) i.e., map: usuario -> tarjeta
* Los datos se reciben en formato JSON
* Los status code a utilizar se encuentra en el RFC HTTP 1.1

![first_flow.svg](first_flow.svg)

#### Requerimiento 2

Al "pasar" la tarjeta por el dispositivo asociado a un servicio se quiere que se actualice el balance de cobro en los datos de la tarjeta.

##### Especificación

Cunado un usuario tiene la tarjeta asignada debe ser capaz de usarla para habilitar los servicios de la habitación. Es necesario que todos estos movimientos se guarden para luego poder ser cobrados.

![second_uml.svg](second_uml.svg)

Para resolver esto habrá que recibir la comunicación del dispositivo que usaremos para leer las tarjetas.
El sistema recibirá información sobre la tarjeta y sobre el servicio, de forma tal que deberá utilizar la información cargada en la base de datos para actualizar el balance. Lo cual podríamos ver de la siguiente forma:

![second_flow.svg](second_flow.svg)

#### Requerimiento 3

Se quiere poder visualizar un reporte de los gastos del usuario.

##### Especificación

El sistema debe ser capaz de mostrar un reporte que permita inferir ciertas cosas acerca de los comportamientos de los usuarios. El reporte debe ser de la siguiente forma:

![mockup.png](mockup.png)

El mockup que se muestra es lo mínimo indispensable, pero cualquier otro chart que se pueda inferir en base a los datos que tengamos será bienvenido.


## Notas

Describir los sistemas externos. todos
los que usan nuestro sistema (facturacion, gestion hotelera)
los que usamos para dar acceso a los servicios
como nos comunicamos con los servicios externos
en que formato y con que peculiaridades

Problema desde el POV del analista

Nuestro cliente tiene la necesidad de controlar, visualizar y analisar los datos de consumo de sus clientes, con el fin de poder cobrar lo justo y necesario que se gasto, poder luego hacer analytics y demas.

El sistema que se pide es simplemente una API, que provee los datos que otro sistema visualizara. Donde se visualiza, quienes lo pueden ver y demás es parte del scope del sistema externo.

* Al entrar al hotel se le da N tarjetas al usuario (1 por familiar mayor de edad), las cuales seran grabadas con un ID unico asociado al cliente, y un ID de habitación. Esta grabación se hara con un lectograbador NFC que posee el administrativo de atencion al usuario.
* Todas las tarjetas pueden acceder a todos los servicios del hotel
* Los servicios del hotel se pueden clasificar dependiendo de su ¿tiempo de uso?:
  * Servicios por dia
  * Servicios por uso de unica vez
* Los diferentes servicios pueden accederse de alguna de las siguientes maneras:
  * Acceso por puerta restringida -> La tarjeta se pasa por un lector que abre la puerta
  * Acceso por actuador ON/OFF -> La tarjeta se pasa por un lector que enciende el aparato
  * En cualquiera de esos casos, nuestro sistema le avisa al sistema externo que se debe desbloquear/encender. Nuestro sistema no sera el encargado de implementar la solucion de desbloquado/encendido.
* El sistema debe devolver los datos de eventos de consumición de servicio asociados a una tarjeta/cliente, va a esperar un ID del cliente, y devolver los datos que se encuentran en la base de datos.
* La tarjeta NFC solo va a guardar los datos de ID de tarjeta y habitación, sin guardar datos de cada una de las transacciones, sera solo utilizada como metodo identificatorio, y para poder guardar en la base de datos el consumo asociado al ID de la tarjeta, es decir, la tarjeta X consumio Y servicio a las Z horas.
 
