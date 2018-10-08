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

##### Fenomenos compartidos controlados por la Maquina

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

##### Fenomenos compartidos controlados por la Maquina

* Se abre la ranura de la máquina.
* Sale el dinero de la ranura.


# Ejercicio 2

## Microondas

#### 1)

##### Ambiente

* El magnetron se encuentra encendido.
* El plato giratorio se encuentra girando.
* La lampara interna se encuentra encendida.

##### Maquina

* El contador de tiempo restante se encuentra en 30 unidades.
* La variable "magnetron_encendido" se encuentra en True o False
* La variable "luz_encendida" se encuentra en True o False
* La variable "plato_girando" se encuentra en True o False
* La variable "magnetron_intensidad" se encuentra en Alto, Bajo o Medio.
* La variable "puerta_abierta" se encuentra en True o False.

##### Compartidos

* El usuario presiona el boton 10m.
* El usuario gira la parellia y la coloca en Medio.
* El usuario presiona el boton "Iniciar".
* El display muestra el valor "00:30".
* El plato comienza a girar.
* La luz interna se enciende.
* El magnetron se enciende.
* El usuario presiona el boton "Abrir puerta".


#### 2)

##### Fenomenos compartidos controlados por el Ambiente

* El usuario presiona el boton 10m.
* El usuario gira la parellia y la coloca en Medio.
* El usuario presiona el boton "Iniciar".
* El usuario presiona el boton "Abrir puerta".

##### Fenomenos compartidos controlados por el Ambiente

* El display muestra el valor "00:30".
* El plato comienza a girar.
* La luz interna se enciende.
* El magnetron se enciende.


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
