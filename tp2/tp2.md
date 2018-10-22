# Trabajo práctico 2

## Problema 1

### Alcance del problema

Se deberá construir una nueva _funcionalidad_ al sistéma de venta de tickets ya existente que permita al usuario _elegir el tipo de comida que quiere consumir en el vuelo_.

El alcance para cumplir con esta nueva funcionalidad será el siguiente:

En principio habrá que investigar y conocer como funcionan las máquinas de check in (si es que hay algunas particulares) para poder determinar como se vá a integrar el software construido.
En segundo lugar habrá que investigar también cómo funciona el sistéma que nos provee información acerca de los menues, los tipos de comida, etc, que se pueden dar en cada vuelo.
Por último, se desarrollará un software que utilize toda la información obtenida para permitirle al usuario elegir el típo de comida que desea consumir en su vuelo, mediante una interfaz gráfica. A su vez esta decisión deberá ser persistida y puesta a disposición de las aerolineas de forma tal que cada una decida qué hacer con dicha decisión.

### Objetos del domínio

> Usuario: Dinámico - Activo - Cooperativo

Es claro que el usuario en este problema, y como es usual, es incontrolable y hace lo que quiere, pero en nuestro contexto él es quién decide cuando y como elegir qué desea comer y actúa como el entry point del sistema en general, así que se puede pensar que esperamos cierta cooperación del mismo.

> Base de datos: Estático

En el contexto del problema se puede pensar que la base de datos o lo que fuera que nos provea información acerca de los vuelos, los usuarios y los menúes es estático ya que si bien todos sabemos que los menúes van cambiando, lo cierto es que en el momento en el que el usuario está decidiendo no hace falta que esos cambios se vean en _tiempo real_.

> Display: Dinámico - Reactivo

El display puede verse como un objeto que cambia en relación a otros eventos (i.e cambia alguna variable en el sistéma, etc)

> Sistema externo de checkin: Dinámico - Activo - Programable

El sistema externo de checkin desde nuestro punto de vista, cambia de estado solo ya que no depende de nada que nosotros podamos controlar, por eso es dinámico-activo. Por otro lado, al ser un sistéma activo, cuenta como programable y no como autónomo o coperativo.


## Problema 2

El problema que elegimos es el de implementar un sistema que sirva para que el usuario final pueda visualizar el estado del pedido para una cadena de comidas rápidas. El sistema debe acoplarse al sistema ya existente.

El alcance incluye hacer la pantalla que refleje el estado de cada pedido basandose en dicho sistema.
Para lograr dicho alcance es necesario investigar como comunicarse con el sistema ya existente, así también como en que formato se publica la info.

### Objetos de domínio

Debido a que el sistema que estamos armando solo necesita consumir datos de otro sistema (donde se cuenta con los estados de los pedidos), y mostrarlos en una pantalla, los únicos dos objetos de dominio son estos anteriormente mencionados, dado que no hay interacción con el usuario final (él vé lo que se muestra en pantalla).

> Sistema Existente: Dinámico - Activo - Autonomo

El sistema existente se encarga de recopilar la información que vamos a usar, de una manera que no nos interesa en nuestro problema, dado que tratamos al sistema existente como una caja negra que nos provee con la información a mostrar en la pantalla.
Debido a que lo tratamos como una caja negra, adquiere por transitividad todas las propiedades de los usuarios, dado que puede cambiar en base al input de los mismos, debido a esto, para nosotros el sistema externo es autonomo.

> Pantalla: Dinámico - Reactivo

Debido a que la pantalla lo único que hace es modificar la matriz de pixeles en base al input que le pasa la maquina (nuestro sistema), consideramos que es un dominio dinamico reactivo, dado que solo reacciona a nuestro input.
