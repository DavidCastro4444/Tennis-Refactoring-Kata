# Tennis Refactoring Kata

_Este proyecto es el resultado de aplicar técnicas de Refactoring y Code Smell, el proyecto raiz que se utilizo como base dle ejercício se puede encontrar en este [Repositorio](https://github.com/emilybache/Tennis-Refactoring-Kata) _

## Para Empezar 🚀

_El proyecto propuesto otorga diferentes clases que permiten indagar en técnicas de Refacotoring para tratar aplicar al mismo proyecto_t

# Tabla de Contenido <a name="indice"></a>
1. [Pre-Requisitos](#preRequisitos)
2. [Ejecución de pruebas](#ejecucionPruebas)
3. [Analice las pruebas end-to-end](#analiceEndToEnd)
    1. [Técnicas Clase TennisGame1](#test1)
    2. [Técnicas Clase TennisGame2](#test2)
    3. [Técnicas Clase TennisGame3](#test3)
    4. [Técnicas Clase TennisGame4](#test4)
4. [Clean Code](#cleanCode)
    1. [Código enfocado](#codigoEnfocado)
    2. [Entendible](#entendible)
    3. [Escalable](#escalable)
    4. [Duplicidad](#duplicidad)
    5. [Testeable](#testeable)
    6. [Principio menor asombro](#principioMenorAsombro)
 5. [Testin Debt](#testinDeb)
    1. [Características](#caracteristicas)
    2. [Estándares de nombramiento](#estandaresNombramiento)
    3. [Concejos](#concejos)
    4. [Malas prácticas](#malasPracticas)
    5. [Pruebas faltantes](#pruebasFaltantes)
 6. [Better Code Hub](#betterCode)
    1. [Pasos](#pasos)
    2. [Resultados](#resultados)
    3. [Write short units of code](#writeShortUnitsOfCode)
    4. [Write Simple Units of code](#writeSimpleUnitsOfCode)
    5. [Write code once](#writeCodeOnce)
    6. [Keep unit interfaces small](#keepUnitInterfacesSmall)
    7. [Separate Concerns in modules](#separateConcernsModules)
    8. [Couple arquitecture components loosely](#coupleArquitecureComponentsLoosely)
    9. [Keep your codebase small](#keepYourCodebaseSmall)
    10. [Automate tests](#automateTest)
    11. [Write clean code](#writeCleanCode)


# Pre-Requisitos <a name="preRequisitos"></a> 📋

_El proyecto corre bajo la versión java 8 mínimo para su compilación_

[Tabla de Contenido](#indice)

## Ejecutando las pruebas <a name="ejecucionPruebas"></a> ⚙️

_El proyecto contiene una clase llamada TennisTest.java en donde se valida que su funcionamiento es el esperado_

La forma para correr la prueba unitaria se aconseja que sea por consola 

```
mvn test
```
[Tabla de Contenido](#indice)
## Analice las pruebas end-to-end <a name="analiceEndToEnd"></a> 🔩

_La prueba hace uso de arrayList con la finalidad de generar diferentes posibles escenarios, una vez dimensionado los puntajes, se hace uso del polimorfismo ppor medio de una interfaz que generar patrones de comportamiento para las clases: TennisGame1, TennisGame2, TennisGame3 y TennisGame4_

```
public interface TennisGame {
    void wonPoint(String playerName);
    String getScore();
}
```
Esto se hace con cada clase
```
public class TennisGame1 implements TennisGame {
```

se hace uso de todas las clases de para hacer uso del método probatorio
```
public void checkAllScores(TennisGame game) {
        int highestScore = Math.max(this.player1Score, this.player2Score);
        for (int i = 0; i < highestScore; i++) {
            if (i < this.player1Score)
                game.wonPoint("player1");
            if (i < this.player2Score)
                game.wonPoint("player2");
        }
        assertEquals(this.expectedScore, game.getScore());
    }
    @Test
    public void checkAllScoresTennisGame1() {
        TennisGame1 game = new TennisGame1("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame2() {
        TennisGame2 game = new TennisGame2("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame3() {
        TennisGame3 game = new TennisGame3("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame4() {
        TennisGame game = new TennisGame4("player1", "player2");
        checkAllScores(game);
    }
```

## Técnicas Clase TennisGame1 <a name="test1"></a>⌨️
_Code smells_

Decompose Conditional en las líneas 26 a 71

Replace Conditional with Polymorphism

Remove Assignments to Parameters


## Técnicas Clase TennisGame2 <a name="test2"></a>⌨️
_Code smells_

Consolidate Duplicate Conditional Fragments en las líneas 18 a 99

Decompose Conditional en las líneas 26 a 71

Replace Conditional with Polymorphism

Remove Assignments to Parameters

## Técnicas Clase TennisGame3 <a name="test3"></a>⌨️

_Code smells_

Extract Variable

## Técnicas Clase TennisGame4 <a name="test4"></a>⌨️

_Code smells_

Extract Variable

[Tabla de Contenido](#indice)

## Clean Code <a name="cleanCode"></a>🚀

_Características relacionadas en el código para visualizar diferentes ejemplos en donde se muestra como tener un clean code_

### Código enfocado <a name="codigoEnfocado"></a>📋

_El proyecto corre bajo la versión java 8 mínimo para su compilación_

```
 @Override
    public TennisResult getResult() {
        if (game.receiverHasWon())
            return new TennisResult("Win for " + game.receiver, "");
        return this.nextResult.getResult();
    }
}
class AdvantageServer implements ResultProvider {
    private final TennisGame4 game;
    private final ResultProvider nextResult;
    public AdvantageServer(TennisGame4 game, ResultProvider nextResult) {
        this.game = game;
        this.nextResult = nextResult;
    }
    @Override
    public TennisResult getResult() {
        if (game.serverHasAdvantage())
            return new TennisResult("Advantage " + game.server, "");
        return this.nextResult.getResult();
    }
```
Se puede visualizar métodos confusoso y que evitan tener un código


## Entendible <a name="entendible"></a>⚙️

_Fragmentos del código en donde no es entendible el inicio de variables por ejemplo _

```
    private int p2;
    private int p1;
    private String p1N;
    private String p2N;
    public TennisGame3(String p1N, String p2N) {
        this.p1N = p1N;
        this.p2N = p2N;
    }
```

### Escalable <a name="escalable"></a>🔩

_Debe ser escrito para el desarrollador y no para las maquinas_

```
 @java.lang.Override
    public String getScore() {
        TennisResult result = new Deuce(
                this, new GameServer(
                        this, new GameReceiver(
                                this, new AdvantageServer(
                                        this, new AdvantageReceiver(
                                                this, new DefaultResult(this)))))).getResult();
        return result.format();
    }
```
Código limpio y claro para futuros arreglos


## Duplicidad <a name="duplicidad"></a>⌨️
_Funciones en donde no queda claro poder establer su uso con solo su nombre o firma_
```
 class Deuce implements ResultProvider {
    private final TennisGame4 game;
    private final ResultProvider nextResult;
    public Deuce(TennisGame4 game, ResultProvider nextResult) {
        this.game = game;
        this.nextResult = nextResult;
    }
    
    class GameServer implements ResultProvider {
    private final TennisGame4 game;
    private final ResultProvider nextResult;
    public GameServer(TennisGame4 game, ResultProvider nextResult) {
        this.game = game;
        this.nextResult = nextResult;
    }
    @Override
    public TennisResult getResult() {
        if (game.serverHasWon())
            return new TennisResult("Win for " + game.server, "");
        return this.nextResult.getResult();
    }
}
    
    class GameReceiver implements ResultProvider {
    private final TennisGame4 game;
    private final ResultProvider nextResult;
    public GameReceiver(TennisGame4 game, ResultProvider nextResult) {
        this.game = game;
        this.nextResult = nextResult;
    }
    @Override
    public TennisResult getResult() {
        if (game.receiverHasWon())
            return new TennisResult("Win for " + game.receiver, "");
        return this.nextResult.getResult();
    }
}
```

### Testeable <a name="testeable"></a>⌨️
_Existe una prueba unitaria en donde se testea todas las clases_
```
@Test
    public void checkAllScoresTennisGame1() {
        TennisGame1 game = new TennisGame1("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame2() {
        TennisGame2 game = new TennisGame2("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame3() {
        TennisGame3 game = new TennisGame3("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame4() {
        TennisGame game = new TennisGame4("player1", "player2");
        checkAllScores(game);
    }
```

### Principio menor asombro <a name="principioMenorAsombro"></a>⌨️

Nombres claros y precisos para métodos
```
public void wonPoint(String playerName) {
  public String getScore() {
```
[Tabla de Contenido](#indice)

# Testin Debt <a name="testinDeb"></a>

Para establecer una afirmación objetiva de código de calidad en nuestro proyecto, es fundamental entender el concepto de deuda técnica por Testing, estableciendo como base,
más no única y ni aseverando que se haga de  forma completa, las pruebas unitarias. Siendo tan importante la claridad y calidad de nuestro código, existen diferentes patrones 
para la creación y seguimiento de nuestro código, algunos de ellos relacionados con metodologías ágiles como se evidencia en esta [página](https://biblioteca.sistedes.es/wp-content/uploads/2016/08/CEDI_2016_paper_139.pdf)

Para este proyecto contamos con una clase de Test, que permite realizar y validar el comportamiento esperado de las diferentes clases utilizadas y 
diseñadas en el proyecto. A continuación se hara un análisis de la intención, calidad y relevancia de la prueba unitara.

## Características <a name="caracteristicas"></a>📑

No existe una definición única que restrinja el diseño de las pruebas unitarias, sin embargo, existen unos principios aceptados de forma generalizada que establecen unos objetivos a cumplir al momento de pretender crear una prueba. Estos principios se conocen como F.I.R.ST. 

✔️ Fast: Su ciclo de vida debe ser corto, tiempo esperado no superior a 5 segundos.

✔️ Isolated: Su ciclo de vida no debe verse afectado por el funcionamiento o comportamiento de ninguna prueba externa o recurso.

✔️ Repeatable: Debe repetirse de manera indefinida y no verse afectado su comportamiento por eso.

✔️ Self Validation: Debe ser auto evaluable, esto quiere decir que la prueba misma representa el resultado y no genera ambigüedad para entenderlo, haciendo que sea false o true.

✔️ Timely: Va relacionado con el ciclo del proyecto, esta característica va relacionada con lo oportuno de la prueba, haciendo hincapié en la creación de pruebas antes de salir a producción como valor mínimo esperado.


## Estándares de nombramiento <a name="estandaresNombramiento"></a>📋

Las pruebas deben mantener un nombre que permita reconocer e identificar el metodo que se pretende probar, el estado a probar y comportamiento esperad.
En este proyecto encontramos la siguiente forma de nombramiento de los test.

```
  @Test
    public void checkAllScoresTennisGame1() {
        TennisGame1 game = new TennisGame1("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame2() {
        TennisGame2 game = new TennisGame2("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame3() {
        TennisGame3 game = new TennisGame3("player1", "player2");
        checkAllScores(game);
    }
    @Test
    public void checkAllScoresTennisGame4() {
        TennisGame game = new TennisGame4("player1", "player2");
        checkAllScores(game);
    }
```
Tenemos un nombre que no corresponde a ningún método de la clase que pretende probar, tenemos un estado que se hace seguimiento y el nombre
de la clase a la que se le esta haciendo la prueba, pero no tenemor su valor esperado.


## Concejos <a name="concejos"></a>⚙️

_Aunque se tienen unos principios claves, estos son algunos concejos al momento de preocuparse por el diseño de pruebas unitarias _

✓ Defina una estrategia adecuada de la práctica de testing
✓ Utilice estándares de nombramiento y prácticas de CleanCodees sus UT
✓ Escriba pruebas unitarias confiables
✓ Convierta esta práctica como una regla
✓ Divide y vencerás. Foco en un escenario a la vez
✓ Mínimos Assertspor test 
✓ No permitan que las pruebas tengan dependencias con servicios externos (Isolated) utilice Mocks
✓ Son pruebas unitarias no deintegración
✓ Promover un cubrimiento alto (Coverage) hasta donde sea posible 
✓ Las pruebas evolucionan a medida que el proyecto evoluciona
✓ Nuevos defectos nuevas pruebas unitarias

## Malas prácticas <a name="malasPracticas"></a>🔩

_Basado en la lógica del proyecto, se identificaron los siguientes errores_

```
 public void checkAllScores(TennisGame game) {
        int highestScore = Math.max(this.player1Score, this.player2Score);
        for (int i = 0; i < highestScore; i++) {
            if (i < this.player1Score)
                game.wonPoint("player1");
            if (i < this.player2Score)
                game.wonPoint("player2");
        }
        assertEquals(this.expectedScore, game.getScore());
    }
```
A pesar de que existe un @Test para cada clase, se evidencia una constante en cada prueba que usa el método mostrado anteriormente, pese
a tener diferentes comportamientos lógicos las clases. Se hace indispensable el diseño adecuado a probar por las diferentes clases
diseañadas


## Pruebas faltantes <a name="pruebasFaltantes"></a>⌨️
_Se debe hacer prueba por los 2 métodos de la interfaz usada, evidenciandose a continuación_
```
 public interface TennisGame {
    void wonPoint(String playerName);
    String getScore();
}
```
[Tabla de Contenido](#indice)

# Better Code Hub <a name="betterCode"></a>

Better Code Hub es un servicio de análisis de código fuente basado en la web que verifica el cumplimiento de una base de código con las diez pautas presentadas en Creación de software mantenible.

![Image text](https://miro.medium.com/max/1400/1*TS-ZTeI7sQS7dy_AlMqSXQ.png)

## Pasos <a name="pasos"></a>📑
Pasos para la configuración  y sincronización herramienta y proyecto

✔️ Crear una cuenta y sincronizar con la cuenta de git por medio de este [enlace](https://bettercodehub.com/).

✔️ Seleccionar el proyecto de la cuenta git para hacer una revisión del código.

✔️ Analizar el resultado de la herramienta.

### Resultados <a name="resultados"></a>📋

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

## Write short units of code <a name="writeShortUnitsOfCode"></a>⚙️

_Las unidades son los grupos de código más pequeños que se pueden mantener y ejecutar de forma independiente. En Java, las unidades son métodos o constructores. Una unidad siempre se ejecuta como un todo. No es posible invocar solo unas pocas líneas de una unidad. Por lo tanto, la pieza de código más pequeña que se puede reutilizar y probar es una unidad. _

Se identificaron 2 errores de unidades de código
```
TennisGame2.getScore()        Lines of code / 78
TennisGame1.getScore()        Lines of code / 54
```
## Write Simple Units of code <a name="writeSimpleUnitsOfCode"></a>⚙️
La complejidad es una característica de calidad a menudo cuestionada. El código que parece complejo para un desarrollador externo o novato puede parecer sencillo para un desarrollador que está íntimamente familiarizado con él. En cierta medida, lo “complejo” está en el ojo del espectador. Sin embargo, hay un punto en el que el código se vuelve tan complejo que modificarlo se convierte en una tarea extremadamente arriesgada y que consume mucho tiempo, y mucho menos probar las modificaciones después. Para mantener el código mantenible, debemos poner un límite a la complejidad. Otra razón para medir la complejidad es conocer el número mínimo de pruebas que necesitamos para estar suficientemente seguros de que el sistema actúa de forma predecible. Antes de que podamos definir un límite de complejidad de código de este tipo, debemos poder medir la complejidad.

Una forma común de evaluar objetivamente la complejidad es contar el número de rutas posibles a través de un fragmento de código. La idea es que cuantos más caminos se puedan distinguir, más complejo será un fragmento de código. Podemos determinar el número de caminos sin ambigüedades contando el número de puntos de bifurcación

```
TennisGame2.getScore()        Lines of code / 78  Branch points / 39
TennisGame1.getScore()        Lines of code / 54  Branch points / 15
TeniisGame3.getscore()        Lines of code / 13  Branch points / 7
```

## Write code once <a name="writeCodeOnce"></a>⚙️
_una filosofía adoptada por un compilador y sus bibliotecas de software asociadas o por una biblioteca de software/ marco de software que se refiere a la capacidad de escribir un programa de computadora que se puede compilar en todas las plataformas sin necesidad de modificar su código fuente_

```
Indicador pasado 
``` 
## Keep unit interfaces small <a name="keepUnitInterfacesSmall"></a> ⚙️

Hay muchas situaciones en la vida diaria de un programador donde las largas listas de parámetros parecen inevitables. En el apuro de hacer las cosas, puede agregar algunos parámetros más a ese método para que funcione en casos excepcionales. Sin embargo, a largo plazo, esta forma de trabajar conducirá a métodos difíciles de mantener y de reutilizar. Para mantener su código mantenible, es esencial evitar largas listas de parámetros o interfaces de unidades, limitando la cantidad de parámetros que tienen


```
Indicador pasado 
``` 
## Separate Concerns in modules <a name="separateConcernsModules"></a>⚙️

Es un principio de diseño para separar un programa de computadora en distintas secciones. Cada sección aborda una preocupación separada , un conjunto de información que afecta el código de un programa de computadora. Una preocupación puede ser tan general como "los detalles del hardware de una aplicación" o tan específica como "el nombre de la clase que se creará"

```
Indicador pasado 
``` 

## Couple arquitecture components loosely <a name="coupleArquitecureComponentsLoosely"></a>⚙️

Tener una visión clara de la arquitectura del software es esencial cuando crea y mantiene software. Una buena arquitectura de software le brinda una idea de lo que hace el sistema, cómo lo hace y cómo se organiza la funcionalidad (es decir, en agrupaciones de componentes). Le muestra la estructura de alto nivel, el "esqueleto", por así decirlo, del sistema. Tener una buena arquitectura hace que sea más fácil encontrar el código fuente que está buscando y comprender cómo interactúan los componentes (de alto nivel) con otros componentes.

![image](https://user-images.githubusercontent.com/26014448/159193506-9cb1348d-4bff-434c-ad58-0770e198d070.png)
![image](https://user-images.githubusercontent.com/26014448/159193521-a3a2edb8-d79d-4709-a7c3-6cccc68fb8f7.png)

## Keep your codebase small <a name="keepYourCodebaseSmall"></a>⚙️
Una base de código es una colección de código fuente que se almacena en un repositorio, se puede compilar e implementar de forma independiente y es mantenida por un equipo. Un sistema tiene al menos una base de código. Los sistemas más grandes a veces tienen más de una base de código. Un ejemplo típico es el software empaquetado. Puede haber una base de código para la funcionalidad estándar, y hay diferentes bases de código mantenidas de forma independiente para complementos específicos del cliente o del mercado.

![image](https://user-images.githubusercontent.com/26014448/159193580-2c6d23e6-5eb3-4c15-8ab3-ffb5c84e8b98.png)

## Automate tests <a name="automateTest"></a>⚙️

En las pruebas de software , la automatización de pruebas es el uso de software separado del software que se está probando para controlar la ejecución de las pruebas y la comparación de los resultados reales con los resultados previstos. [1] La automatización de pruebas puede automatizar algunas tareas repetitivas pero necesarias en un proceso de prueba formalizado que ya existe, o realizar pruebas adicionales que serían difíciles de realizar manualmente. La automatización de pruebas es fundamental para la entrega continua y las pruebas continuas

![image](https://user-images.githubusercontent.com/26014448/159193676-41d04c72-68f8-48a8-ad8f-fa6f693781e2.png)

## Write clean code <a name="writeCleanCode"></a>⚙️

Se considera que el código es limpio (en inglés, clean code) cuando es fácil de leer y entender. Si resuelve los problemas sin agregar complejidad innecesaria, permitiendo que el mantenimiento o las adaptaciones, por algún cambio de requerimiento, sean tareas más sencillas, entonces estamos hablando de “clean code”.

Para crear código limpio hay que conocer y poner en práctica un conjunto de principios o técnicas de desarrollo que nos ayudarán a evitar los code smells, es decir, esos síntomas de un programa que te dan el indicio de que existe un problema más profundo.


```
Indicador pasado 
``` 
[Tabla de Contenido](#indice)


## Autores ✒️

_Participantes_

* **Trabajo Base** - *Trabajo Inicial* - [David Castro](https://github.com/DavidCastro4444)

## Licencia 📄

Este proyecto está bajo la Licencia (Tu Licencia) - mira el archivo [LICENSE.md](LICENSE.md) para detalles

## Expresiones de Gratitud 🎁

* Comenta a otros sobre este proyecto 📢    
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.
* etc.



---
⌨️ con ❤️ por [David Castro](https://github.com/DavidCastro4444) 😊
