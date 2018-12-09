# Trabajo práctico 3

## Sistema de cobro por tarjeta NFC
--------
### Cliente

Hoteles Pepito es una cadena de hoteles que quiere implementar un sistema de manejo de servicios en el cual sus clientes puedan elegir qué servicios utilizar y luego reciban una factura acorde de forma sencilla y rápida. 

#### Requerimientos de negocio

##### Contexto

Hoteles Pepito, tiene los siguientes servicios adicionales al hospedaje:

1) Gimnasio
2) Pileta
3) Jacuzzi
4) Bar
5) Salon de Juegos
6) Heladera
7) Caja Fuerte
8) Sauna
9) Spa
10) Restaurante

Cada uno de estos servicios se cobra a parte del precio del hospedaje, lo que quiere decir que si uno pide una habitación con _3_ y _7_, al final de la estadía deberá pagar la suma de los precios del hospedaje, del jacuzzi y de la caja fuerte, lo haya usado o no. Hay algunos de estos servicios que están fuera de las habitaciones, y para usarlos, los huespedes tienen que pedir unas credenciales al personal administrativo. De esta forma se lleva un registro de los servicios que usó cada huesped para realizar la facturación al final. Todo esto se hace mediante un sistema de facturación que recibe _eventos_ (i.e., "el huesped X pidió usar el gimnacio", "el huesped X pidió usar el Salón de Juegos", etc)

##### Oportunidad de negocio, criterios de éxito, y necesidades del mercado.

Segun Hoteles Pepito, los clientes están satisfechos con la idea de pagar por lo que usan en cuanto a los servicios que estan afuera de las habitaciones, no así con pagar todo lo que tenga la habitación. Por otro lado, los clientes también acusan que tener que ir hasta la sala de entrada a pedir credenciales por un servicio es un tanto molesto a pesar de las ventajas antes mencionadas.

Por este motivo, Hoteles Pepito quiere ofrecerles a sus clientes una forma mejor y más personalisada de gestionar sus gastos, sin generarles tantas molestias.

En pocas palabras, las necesidades del cliente y el criterio de éxito yacen en que los clientes de Hoteles Pepito puedan tener más libertad a la hora de utilizar los servicios.

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
 
