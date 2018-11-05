# Trabajo práctico 3

## Centralizar el sistema de pago de los hoteles
------
### Contexto

En el pasado semestre, particularmente durante la epoca de invierno, el equipo de marketing y logistica tuvieron el encargo de realizar encuestas a razon de adquirir, y analizar los diferentes comportamientos de los clientes. Dichas encuestas revelaron que los usuarios no confían en los sistemas de pagos que ofrecen los hoteles, y las razones son bastante variadas. Algunos de los ejemplos obtenidos son sistemas deficientes, sistemas con respuesta que tardan demasiado tiempo, etc. Por otro lado, uno de los servicios habituales que nuestra gama de hoteles suele manejar es la venta inmediata y/o diferida de paquetes turisticos,

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



Si bien, se lleva utilizando el sistema actual durante un tiempo prolongado, tambien es de publico conocimiento que los avances tecnologicos actuales pueden beneficiar a la empresa de diferetes maneras. Nuestro principal objetivo a mediano/largo plazo es generar un sistema centralizado

Por este motivo, se quiere realizar un sistema que permita centralizar los metodos de pago, de forma tal que los clientes puedan confiar en que no les van a cobrar algo que no utilizaron además de que los hoteles también puedan confiar en que la gente no se salteará ningún servicio utilizado.

### Alcance

El alcance, será el de integrar en cada uno de los hoteles los dispositivos que permitiran acercar una tarjeta magnética para habilitarlos (i.e para abrir el bar, etc). De esta forma se sabrá cuales fueron los servicios utilizados para la hora del cobro.

Por otro lado, también habrá que hacer un sistema que pueda leer los datos de la tarjeta magnética para luego comunicarse con los sistemas de cobro existentes (e.g visa, mastercard, etc) para realizar finalmente el cobro.

Finalmente, vemos una oportunidad de negocio en tratar los datos de los usuarios (i.e qué servicios usan y cuales no), por lo que esto también será parte del alcance.

