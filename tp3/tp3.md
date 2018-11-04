# Trabajo práctico 3

## Centralizar el sistema de pago de los hoteles
------
### Contexto

Últimamente los hoteles realizaron una serie de encuestas que reveló que los usuarios no confían en los sistemas de pagos que ofrecen los hoteles. Por otro lado, muchas vecesse ofrecen distintos _paquetes_ (1) según los servicios que quieran tener los clientes, los cuales a veces se aprovechan y obtienen de todas formas sin pagarlos.

(1) Por ejemplo:
|básico|bar   |jacuzzi|heladera
|:----:|:----:|:-----:|:---:
|10 u$s|5 u$s |10 u$s  |10 u$s

Por este motivo, se quiere realizar un sistema que permita centralizar los metodos de pago, de forma tal que los clientes puedan confiar en que no les van a cobrar algo que no utilizaron además de que los hoteles también puedan confiar en que la gente no se salteará ningún servicio utilizado.

### Alcance

El alcance, será el de integrar en cada uno de los hoteles los dispositivos que permitiran acercar una tarjeta magnética para habilitarlos (i.e para abrir el bar, etc). De esta forma se sabrá cuales fueron los servicios utilizados para la hora del cobro.

Por otro lado, también habrá que hacer un sistema que pueda leer los datos de la tarjeta magnética para luego comunicarse con los sistemas de cobro existentes (e.g visa, mastercard, etc) para realizar finalmente el cobro.

Finalmente, vemos una oportunidad de negocio en tratar los datos de los usuarios (i.e qué servicios usan y cuales no), por lo que esto también será parte del alcance.

