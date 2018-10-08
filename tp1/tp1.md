# Ejercicio 1

## Cajero automático

El problema puede separarse en varias partes, de las cuales nosotros vamos a elegir dos, ya que es lo que nos pareció más razonable.


### Consultar saldo
#### 1)
##### Ambiente

* El usuario quiere conocer su saldo.
* El banco (o la entidad pertinente) mantiene los estados de las cuentas de cada uno de los usuarios.
* El display se encuentra conectado.

##### Máquina

* Los pines saldo(Usuario) marcan 00011101010101011010.
* El router de pantallas se encuentra en la pantalla inicial.
* El router de pantallas se encuentra en la pantalla de consulta de saldo.

##### Compartidos

* El usuario ingresa la tarjeta.
* El usuario presiona el boton "Consultar saldo"
* El display marca $938,90.

#### 2)

##### Fenomenos compartidos controlados por el Ambiente

* El usuario ingresa la tarjeta.
* El usuario presiona el boton "Consultar saldo"

##### Fenomenos compartidos controlados por el Ambiente

* El display marca $938,90.

### Retirar cantidad de dinero seleccionada
#### 1)
##### Ambiente

* El usuario quiere retirar dinero.
* El banco (o la entidad pertinente) mantiene los estados de las cuentas de cada uno de los usuarios.
* Algun billete se rompe cuando sale de la ranura.
* El usuario se vá antes de retirar el dinero.

##### Máquina

* puede_retirar_cantidad(Usuario, Cantidad) está en False o True.
* Los pines saldo(Usuario) marcan 00011101010101011010.
* La variable ranura_abierta está en False o True.
* Se avisa al banco que reste cierto dinero a la cuenta del usuario.


##### Compartidos

* El usuario ingresa la tarjeta.
* El usuario ingresa "retirar $1000".
* Se abre la ranura de la máquina.
* Sale el dinero de la ranura.

#### 2)

##### Fenomenos compartidos controlados por el Ambiente

* El usuario ingresa la tarjeta.
* El usuario ingresa "retirar $1000".

##### Fenomenos compartidos controlados por el Ambiente

* Se abre la ranura de la máquina.
* Sale el dinero de la ranura.


# Ejercicio 2
## Microondas

En este ejercicio vamos a hacer también la separación en el análisis, pero no la vamos a desarrollar, ya que no es parte del ejercicio.


#### 1)

| Ambiente | Máquina  | Compartido |
|----------|----------|------------|
| Intensidad de coccion asociado a potencia indicada al magnetron | Potencia :: Alto \| Medio \| Bajo | Potencia magnetron <--> Variable Potencia |
| El usuario toca iniciar | PuertaAbierta :: Boolean | El magnetron genera ondas => ¬PuertaAbierta ^ El usuario toco iniciar   |
| Giro del plato vinculado a la func del motor | Motor :: Off \| 1 \| 2 \| 3  | Giro del plato <-> Motor >= 1 |
| Estado de la lampara interna en funcion del sensor de la puerta | Lampara :: Boolean | PuertaAbierta => Lampara |
| La puerta está abierta/cerrada | PuertaAbierta :: Boolean | Puerta abierta/cerrada <--> PuertaAbierta = True \| False |
| El display vinculado al tiempo que lleva encendido el motor | CookTime :: NonNegInteger | Display muestra x <-> CookTime = x |

#### 2)

La potencia del magnetrón es controlada por el ambiente ya que la variable está ligada al potenciómetro físico.
El giro del plato es controlado por la máquina como una reacción al fenómeno del ambiente en el que se toca el botón de iniciar.
El estado de la lampara es un fenómeno controlado por el ambiente, dado que está ligado enteramente con el estado de la puerta.
El display es controlado por la máquina dado que está ligado claramente a la variable CookTime.

#### 3)

Sin ser extensivos, los requerimientos básicos que pudimos pensar son los siguientes:

* Que al presionar iniciar, luego de establecer el tiempo y estando la puerta cerrada, comience a calentar.
* Que no arranque si la puerta se encuentra abierta.
* Que el plato gire al calentar.
* Que se detenga al presionar parar.
* Que se detenga al presionar abrir puerta.
* Que funcione durante el tiempo seleccionado y luego se detenga.
* Que caliente a la potencia seleccionada.
* Que se encienda la lámpara al inicia y se apague al finalizar.
* Poder definir el tiempo de calentamiento entre 1 segundo y 99:59 minutos.
* Que el display muestre el tiempo restante de coccionn.
