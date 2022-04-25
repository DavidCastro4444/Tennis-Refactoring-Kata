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
 7. [Continuos Integration](#continuosIntegration)
    1. [CI usando GitHub Actions](#ciGitHub)
    2. [File YAML](#fileYaml)
    3. [Name](#name)
    4. [On](#on)
    5. [Filtros](#filtros)
    6. [On.<pull_request|pull_request_target>.<branches|branches-ignore>](#onPull)
    7. [Jobs](#jobs)
    8. [Build](#build)
    9. [Análisis de código](#analisisCodigo)
    10. [Pruebas](#pruebas)
  


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

# Continuos Integration <a name="continuosIntegration"></a>

La integración continua (CI) es una práctica de software que requiere enviar código con frecuencia a un repositorio compartido. Confirmar código con mayor frecuencia detecta errores antes y reduce la cantidad de código que un desarrollador necesita depurar para encontrar el origen de un error. Las actualizaciones frecuentes de código también facilitan la combinación de cambios de diferentes miembros de un equipo de desarrollo de software. Esto es excelente para los desarrolladores, que pueden pasar más tiempo escribiendo código y menos tiempo depurando errores o resolviendo conflictos de fusión.

Cuando confirma código en su repositorio, puede compilar y probar continuamente el código para asegurarse de que la confirmación no introduzca errores. Sus pruebas pueden incluir filtros de código (que verifican el formato de estilo), controles de seguridad, cobertura de código, pruebas funcionales y otros controles personalizados.

Construir y probar su código requiere un servidor. Puede compilar y probar actualizaciones localmente antes de enviar el código a un repositorio, o puede usar un servidor de CI que verifica las nuevas confirmaciones de código en un repositorio.

## CI usando GitHub Actions <a name="ciGitHub"></a>🚀

CI usando GitHub Actions ofrece flujos de trabajo que pueden construir el código en su repositorio y ejecutar sus pruebas. Los flujos de trabajo pueden ejecutarse en máquinas virtuales alojadas en GitHub o en máquinas que usted mismo aloja.

Puede configurar su flujo de trabajo de CI para que se ejecute cuando se produzca un evento de GitHub (por ejemplo, cuando se inserte código nuevo en su repositorio), en un horario establecido o cuando se produzca un evento externo mediante el webhook de distribución del repositorio.

GitHub ejecuta sus pruebas de CI y proporciona los resultados de cada prueba en la solicitud de extracción, para que pueda ver si el cambio en su rama introduce un error. Cuando todas las pruebas de CI en un flujo de trabajo pasan, los cambios que impulsó están listos para ser revisados por un miembro del equipo o combinados. Cuando falla una prueba, uno de sus cambios puede haber causado la falla.

###  File YAML <a name="fileYaml"></a>📋
Los archivos de flujo de trabajo utilizan la sintaxis YAML y deben tener una extensión de archivo .ymlo .yaml
Debe almacenar archivos de flujo de trabajo en el .github/workflowsdirectorio de su repositorio.

## Name <a name="name"></a>⚙️

El nombre de su flujo de trabajo. GitHub muestra los nombres de sus flujos de trabajo en la página de acciones de su repositorio. Si omite name, GitHub lo establece en la ruta del archivo de flujo de trabajo en relación con la raíz del repositorio.

La forma para correr la prueba unitaria se aconseja que sea por consola 

```
name: Build
```

### On <a name="on"></a>🔩

Para desencadenar automáticamente un flujo de trabajo, use onpara definir qué eventos pueden hacer que se ejecute el flujo de trabajo.

Puede definir eventos únicos o múltiples que pueden desencadenar un flujo de trabajo o establecer un cronograma. También puede restringir la ejecución de un flujo de trabajo para que solo se produzca en archivos, etiquetas o cambios de rama específicos. 

```
name: Build
on:
```

### Filtros <a name="filtros"></a>⌨️

Algunos eventos tienen filtros que le brindan más control sobre cuándo debe ejecutarse su flujo de trabajo.

Por ejemplo, el pushevento tiene un branchesfiltro que hace que su flujo de trabajo se ejecute solo cuando se produce una inserción en una rama que coincide con el branchesfiltro, en lugar de cuando se produce cualquier inserción.

```
name: Build
on:
  push:
    branches:
      - main
```

### on.<pull_request|pull_request_target>.<branches|branches-ignore> <a name="onPull"></a>⌨️ 

Al usar los eventos pull_requesty pull_request_target, puede configurar un workflow para que se ejecute solo para solicitudes de extracción dirigidas a ramas específicas.

Utilice el branchesfiltro cuando desee incluir patrones de nombres de sucursales o cuando desee incluir y excluir patrones de nombres de sucursales. Utilice el branches-ignorefiltro cuando solo desee excluir patrones de nombre de rama. No puede usar los filtros branchesy branches-ignorepara el mismo evento en un flujo de trabajo.

Si define tanto branches/ branches-ignorecomo paths, el flujo de trabajo solo se ejecutará cuando se cumplan ambos filtros.

Las palabras clave branchesy branches-ignoreaceptan patrones globales que usan caracteres como *, **, +, ?y !otros para hacer coincidir más de un nombre de rama. Si un nombre contiene alguno de estos caracteres y desea una coincidencia literal, debe escapar de cada uno de estos caracteres especiales con \. 

```
name: Build
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened]
```
### Jobs <a name="jobs"></a>⌨️
Un job es un conjunto de pasos en un workflow que se ejecutan en el mismo ejecutor. Cada paso es un script de shell que se ejecutará o una acción que se ejecutará. Los pasos se ejecutan en orden y dependen unos de otros. Dado que cada paso se ejecuta en el mismo corredor, puede compartir datos de un paso a otro. Por ejemplo, puede tener un paso que cree su aplicación seguido de un paso que pruebe la aplicación que se creó.

Puede configurar las dependencias de un trabajo con otros trabajos; de forma predeterminada, los trabajos no tienen dependencias y se ejecutan en paralelo entre sí. Cuando un trabajo depende de otro trabajo, esperará a que se complete el trabajo dependiente antes de poder ejecutarse. Por ejemplo, puede tener varios trabajos de compilación para diferentes arquitecturas que no tienen dependencias y un trabajo de empaquetado que depende de esos trabajos. Los trabajos de compilación se ejecutarán en paralelo y, cuando se hayan completado correctamente, se ejecutará el trabajo de empaquetado.


```
name: Build
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened]
jobs:
```
### Build <a name="build"></a>⌨️

Al construir nuestro proyecto, se estipulan pasos como versión, máquina virtuál, dependencias o cualquiér catacterística que sea necesaria para correr el proyecto. Por esta razón, dentro del jobs en el scope de build, se cinfiguran estas características

```
name: Build
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened]
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0  # Shallow clones should be disabled for a better relevancy of analysis
      - name: Set up JDK 11
        uses: actions/setup-java@v1
        with:
          java-version: 11
```
### Análisis de código <a name="analisisCodigo"></a>⌨️

Una característica importante, es la capacidad de automatizar el análisis de código a nuestro proyecto, este facilita la calidad de nuestro repositorio y verificar inconsistencias a tendencias establecidas

```
name: Build
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened]
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0  # Shallow clones should be disabled for a better relevancy of analysis
      - name: Set up JDK 11
        uses: actions/setup-java@v1
        with:
          java-version: 11
      - name: Cache SonarCloud packages
        uses: actions/cache@v1
        with:
          path: ~/.sonar/cache
          key: ${{ runner.os }}-sonar
          restore-keys: ${{ runner.os }}-sonar
```

### Pruebas <a name="pruebas"></a>⌨️

Nuestro proyecto debe contar con un escenarios de pruebas, para esta funcionalidad se realiza una actividad programable dentro del workflow, sistematizando las pruebas y ejecutandolas de manera automática.
 
 
```
name: Build
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened]
jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0  # Shallow clones should be disabled for a better relevancy of analysis
      - name: Set up JDK 11
        uses: actions/setup-java@v1
        with:
          java-version: 11
      - name: Cache SonarCloud packages
        uses: actions/cache@v1
        with:
          path: ~/.sonar/cache
          key: ${{ runner.os }}-sonar
          restore-keys: ${{ runner.os }}-sonar
      - name: Cache Maven packages
        uses: actions/cache@v1
        with:
          path: ~/.m2
          key: ${{ runner.os }}-m2-${{ hashFiles('**/pom.xml') }}
          restore-keys: ${{ runner.os }}-m2
      - name: Build and analyze
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}  # Needed to get PR information, if any
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
        run: mvn -B verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=DavidCastro4444_Tennis-Refactoring-Kata
  test:
    needs: build
    runs-on: ubuntu-latest
    strategy:
      matrix:
        os: [ubuntu-latest, windows-2016]
        node-version: [12.x, 14.x]
    steps:
    - uses: actions/checkout@v2
    - uses: actions/download-artifact@main
      with: 
        name: webpack artifacts
        path: public   
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
