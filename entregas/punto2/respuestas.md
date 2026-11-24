# Principios y patrones de diseño de software

## 1. Elegir un principio SOLID, explicar en qué consiste, describir un caso en el que se viola y cómo corregirlo

Elegiría el principio **Single Responsibility Principle (SRP)** o
principio de responsabilidad única. Este establece que una clase debe
tener una sola responsabilidad, es decir, una única razón para cambiar.
La idea es que cada clase tenga una función bien definida y no termine
encargándose de tareas que no le corresponden.

Por ejemplo, imaginemos una clase `UsuarioService` que se encarga de
registrar usuarios, validar sus datos, guardarlos en la base de datos y
enviar correos de bienvenida. Aquí estamos mezclando varias
responsabilidades en una sola clase, por lo que cualquier cambio en el
envío de correos o en la forma de almacenar los datos podría afectar al
servicio completo.

Para corregirlo, dividiría esas responsabilidades en clases
independientes, como `UsuarioService`, `UsuarioRepository`,
`EmailService` y `UsuarioValidator`. Así, cada clase se encarga de una
tarea específica, lo que facilita el mantenimiento, las pruebas y la
posibilidad de realizar cambios sin afectar otras funcionalidades.

## 2. ¿Qué es la inyección de dependencias (Dependency Injection)? ¿En qué escenarios usarla?

La inyección de dependencias consiste básicamente en que una clase
reciba desde afuera las herramientas u objetos que necesita para
funcionar, en lugar de crearlos por su cuenta. Esto permite que las
clases no dependan directamente de una implementación específica y que
podamos cambiar una dependencia sin tener que modificar toda la lógica
del sistema.

Se utilizaría principalmente cuando trabajamos con servicios externos,
cuando necesitamos cambiar fácilmente una implementación por otra o
cuando queremos hacer pruebas sin depender de servicios reales. Por
ejemplo, podemos simular un servicio de pagos para probar nuestro código
sin realizar transacciones de verdad.

## 3. ¿Cuál es la diferencia entre complejidad esencial y complejidad accidental? Dar un ejemplo de complejidad accidental introducida por una mala decisión de diseño.

La complejidad esencial es aquella que viene del problema que estamos
intentando resolver y que no podemos eliminar porque hace parte de la
naturaleza del negocio. Por otro lado, la complejidad accidental es
aquella que nosotros mismos introducimos debido a malas decisiones de
diseño, implementaciones innecesariamente complicadas o herramientas
inadecuadas.

Por ejemplo, desarrollar un sistema bancario tiene una complejidad
esencial porque debemos manejar transacciones, saldos, seguridad y
reglas financieras. Sin embargo, si para resolver ese problema creamos
demasiadas capas innecesarias, duplicamos código o hacemos que muchas
clases dependan directamente unas de otras, estamos introduciendo
complejidad accidental.

La idea es que como desarrolladores debemos intentar reducir esa
complejidad adicional, utilizando diseños sencillos, evitando la
sobreingeniería y aplicando buenas prácticas. En otras palabras, no
podemos eliminar la dificultad propia del problema, pero sí podemos
evitar complicarlo más de lo necesario con nuestras decisiones técnicas.

## 4. Explicar el modelo de vistas 4+1 de Kruchten. ¿Para qué sirve cada vista?

El modelo 4+1 de Kruchten es una forma de representar la arquitectura de
un sistema de software desde diferentes perspectivas. Se utiliza porque
un sistema puede ser entendido de distintas maneras dependiendo de si lo
estamos viendo desde el punto de vista funcional, del código, de su
ejecución o de la infraestructura donde está desplegado.

El modelo está compuesto por cinco vistas. La vista lógica representa
las funcionalidades del sistema y sus principales clases, objetos y
relaciones. La vista de desarrollo/implementación muestra cómo está
organizado el código fuente, sus módulos y componentes. La vista de
procesos describe cómo funciona el sistema durante su ejecución,
incluyendo la comunicación entre procesos y la concurrencia. La vista
física o de despliegue muestra cómo se distribuye el sistema en
servidores, dispositivos o infraestructura. Finalmente, tenemos la vista
de escenarios (+1), que utiliza casos de uso para relacionar y validar
las otras cuatro vistas.

Este modelo sirve principalmente para documentar y comunicar la
arquitectura de software, ya que permite entender el sistema desde
diferentes perspectivas y facilita que desarrolladores, arquitectos y
otros participantes tengan una visión más completa de cómo está
construido.

## 5. Explicar el patrón Strategy. ¿Cuándo usarlo y qué ventaja tiene frente a muchos if/else o switch?

El patrón **Strategy** consiste en tener diferentes formas de realizar
una misma tarea, encapsulando cada una de ellas por separado para poder
elegir cuál utilizar sin tener que cambiar el funcionamiento principal
del sistema. En palabras más sencillas, se trata de separar cada forma
de hacer algo en su propia lógica, de manera que podamos intercambiarlas
fácilmente según lo que necesitemos, sin afectar el resto del código.

Por ejemplo, una tienda virtual que ofrece diferentes métodos de envío:
estándar, express e internacional. Cada uno tiene una forma diferente de
calcular el costo. En lugar de tener muchos **if/else** para revisar qué
tipo de envío eligió el usuario y ejecutar una lógica diferente, podemos
crear una estrategia para cada tipo de envío y utilizar la que
corresponda.

Se utilizaría cuando tenemos una funcionalidad que puede comportarse de
diferentes maneras dependiendo de la situación y queremos que sea fácil
agregar nuevas opciones en el futuro.

La principal ventaja frente a utilizar muchos **if/else** o **switch**
es que evitamos tener toda la lógica mezclada en una sola parte del
código. Así, si mañana necesitamos agregar un nuevo método de envío,
simplemente creamos una nueva estrategia sin tener que modificar todo lo
que ya existe. En pocas palabras, Strategy permite tener diferentes
maneras de hacer una misma tarea, elegir la que necesitamos y mantener
el código más organizado, flexible y fácil de modificar.

## 6. Diferenciar Adapter y Facade. Si hubiera que integrar un proveedor externo (pagos, correo, identity provider), ¿cuál elegir y por qué?

Aunque Adapter y Facade son patrones estructurales, tienen objetivos
diferentes.

El patrón **Adapter** se utiliza cuando necesitamos conectar dos
componentes que tienen interfaces diferentes o incompatibles. Funciona
como un intermediario que adapta la forma en que nuestra aplicación se
comunica con otro sistema. Por ejemplo, si la aplicación espera trabajar
con una interfaz llamada `PaymentProvider`, pero el proveedor externo
tiene métodos y estructuras diferentes, se puede crear un
`PayPalAdapter` que traduzca las llamadas de nuestra aplicación a las
operaciones que ofrece PayPal.

Por otro lado, el patrón **Facade** busca simplificar la interacción con
un conjunto de clases o servicios que pueden ser complejos. En lugar de
que la aplicación tenga que comunicarse directamente con varios
componentes, se crea una interfaz más sencilla que se encarga de
coordinar esas operaciones. Por ejemplo, al realizar una compra es
necesario validar el inventario, procesar el pago, generar una factura y
enviar una notificación. Una clase `PurchaseFacade` podría coordinar
todos esos procesos y exponer un único método como `completePurchase()`.

En caso de integrar un proveedor externo de pagos, correo o identidad,
la opción **Adapter** es la más adecuada, porque permite adaptar la
interfaz del proveedor a la que utiliza la aplicación, evitando que la
lógica de negocio dependa directamente de los detalles específicos de
ese proveedor. Así, si en el futuro se decide cambiar de PayPal a otro
proveedor, se puede crear un nuevo Adapter sin tener que modificar la
lógica principal del sistema. Sin embargo, también se podría utilizar
Facade si es necesario simplificar o coordinar la interacción con varios
servicios.
