# Better Code Hub

Better Code Hub es un servicio de análisis de código fuente basado en la web que verifica el cumplimiento de una base de código con las diez pautas presentadas en Creación de software mantenible.

![Image text](https://miro.medium.com/max/1400/1*TS-ZTeI7sQS7dy_AlMqSXQ.png)

## Pasos 📑
Pasos para la configuración  y sincronización herramienta y proyecto

✔️ Crear una cuenta y sincronizar con la cuenta de git por medio de este [enlace](https://bettercodehub.com/).

✔️ Seleccionar el proyecto de la cuenta git para hacer una revisión del código.

✔️ Analizar el resultado de la herramienta.

### Resultados 📋

Encontramos diferentes tópicos arojados por el aplicativo.

✔️ Write short units of code.

✔️ Write simple units of code.

✔️ Write code once.

✔️ Keep unit interfaces small.

✔️ Separate concerns in modules.

✔️ Couple architecture components loosely.

✔️ Keep architecture components balanced.

✔️ Keep your codebase small.

✔️ Automate tests.

✔️ Write clean code.

## Write short units of code ⚙️

_Las unidades son los grupos de código más pequeños que se pueden mantener y ejecutar de forma independiente. En Java, las unidades son métodos o constructores. Una unidad siempre se ejecuta como un todo. No es posible invocar solo unas pocas líneas de una unidad. Por lo tanto, la pieza de código más pequeña que se puede reutilizar y probar es una unidad. _

Se identificaron 2 errores de unidades de código
```
TennisGame2.getScore()        Lines of code / 78

TennisGame1.getScore()        Lines of code / 54
```
## Write Simple Units of code ⚙️
La complejidad es una característica de calidad a menudo cuestionada. El código que parece complejo para un desarrollador externo o novato puede parecer sencillo para un desarrollador que está íntimamente familiarizado con él. En cierta medida, lo “complejo” está en el ojo del espectador. Sin embargo, hay un punto en el que el código se vuelve tan complejo que modificarlo se convierte en una tarea extremadamente arriesgada y que consume mucho tiempo, y mucho menos probar las modificaciones después. Para mantener el código mantenible, debemos poner un límite a la complejidad. Otra razón para medir la complejidad es conocer el número mínimo de pruebas que necesitamos para estar suficientemente seguros de que el sistema actúa de forma predecible. Antes de que podamos definir un límite de complejidad de código de este tipo, debemos poder medir la complejidad.

Una forma común de evaluar objetivamente la complejidad es contar el número de rutas posibles a través de un fragmento de código. La idea es que cuantos más caminos se puedan distinguir, más complejo será un fragmento de código. Podemos determinar el número de caminos sin ambigüedades contando el número de puntos de bifurcación

```
TennisGame2.getScore()        Lines of code / 78  Branch points / 39

TennisGame1.getScore()        Lines of code / 54  Branch points / 15

TeniisGame3.getscore()        Lines of code / 13  Branch points / 7
```

## Write code once ⚙️
_una filosofía adoptada por un compilador y sus bibliotecas de software asociadas o por una biblioteca de software/ marco de software que se refiere a la capacidad de escribir un programa de computadora que se puede compilar en todas las plataformas sin necesidad de modificar su código fuente_

```
Indicador pasado 

``` 
## Keep unit interfaces small ⚙️

Hay muchas situaciones en la vida diaria de un programador donde las largas listas de parámetros parecen inevitables. En el apuro de hacer las cosas, puede agregar algunos parámetros más a ese método para que funcione en casos excepcionales. Sin embargo, a largo plazo, esta forma de trabajar conducirá a métodos difíciles de mantener y de reutilizar. Para mantener su código mantenible, es esencial evitar largas listas de parámetros o interfaces de unidades, limitando la cantidad de parámetros que tienen


```
Indicador pasado 

``` 
## Separate Concerns in modules ⚙️

Es un principio de diseño para separar un programa de computadora en distintas secciones. Cada sección aborda una preocupación separada , un conjunto de información que afecta el código de un programa de computadora. Una preocupación puede ser tan general como "los detalles del hardware de una aplicación" o tan específica como "el nombre de la clase que se creará"

```
Indicador pasado 

``` 

## Couple arquitecture components loosely ⚙️

Tener una visión clara de la arquitectura del software es esencial cuando crea y mantiene software. Una buena arquitectura de software le brinda una idea de lo que hace el sistema, cómo lo hace y cómo se organiza la funcionalidad (es decir, en agrupaciones de componentes). Le muestra la estructura de alto nivel, el "esqueleto", por así decirlo, del sistema. Tener una buena arquitectura hace que sea más fácil encontrar el código fuente que está buscando y comprender cómo interactúan los componentes (de alto nivel) con otros componentes.

![image](https://user-images.githubusercontent.com/26014448/159193506-9cb1348d-4bff-434c-ad58-0770e198d070.png)
![image](https://user-images.githubusercontent.com/26014448/159193521-a3a2edb8-d79d-4709-a7c3-6cccc68fb8f7.png)

## Keep your codebase small ⚙️
Una base de código es una colección de código fuente que se almacena en un repositorio, se puede compilar e implementar de forma independiente y es mantenida por un equipo. Un sistema tiene al menos una base de código. Los sistemas más grandes a veces tienen más de una base de código. Un ejemplo típico es el software empaquetado. Puede haber una base de código para la funcionalidad estándar, y hay diferentes bases de código mantenidas de forma independiente para complementos específicos del cliente o del mercado.

![image](https://user-images.githubusercontent.com/26014448/159193580-2c6d23e6-5eb3-4c15-8ab3-ffb5c84e8b98.png)

## Automate tests ⚙️

En las pruebas de software , la automatización de pruebas es el uso de software separado del software que se está probando para controlar la ejecución de las pruebas y la comparación de los resultados reales con los resultados previstos. [1] La automatización de pruebas puede automatizar algunas tareas repetitivas pero necesarias en un proceso de prueba formalizado que ya existe, o realizar pruebas adicionales que serían difíciles de realizar manualmente. La automatización de pruebas es fundamental para la entrega continua y las pruebas continuas

![image](https://user-images.githubusercontent.com/26014448/159193676-41d04c72-68f8-48a8-ad8f-fa6f693781e2.png)

## Write clean code ⚙️

Se considera que el código es limpio (en inglés, clean code) cuando es fácil de leer y entender. Si resuelve los problemas sin agregar complejidad innecesaria, permitiendo que el mantenimiento o las adaptaciones, por algún cambio de requerimiento, sean tareas más sencillas, entonces estamos hablando de “clean code”.

Para crear código limpio hay que conocer y poner en práctica un conjunto de principios o técnicas de desarrollo que nos ayudarán a evitar los code smells, es decir, esos síntomas de un programa que te dan el indicio de que existe un problema más profundo.


```
Indicador pasado 

``` 

## Autores ✒️

_Participantes_

* **Trabajo Base** - *Trabajo Inicial* - [David Castro](https://github.com/DavidCastro4444)

## Licencia 📄

## Expresiones de Gratitud 🎁

* Comenta a otros sobre este proyecto 📢    
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.
* etc.



---
⌨️ con ❤️ por [David Castro](https://github.com/DavidCastro4444) 😊



© 2022 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About

