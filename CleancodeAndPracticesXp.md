# Tennis Refactoring Kata

_Este proyecto es el resultado de aplicar técnicas de Refactoring y Code Smell, el proyecto raiz que se utilizo como base dle ejercício se puede encontrar en este [Repositorio](https://github.com/emilybache/Tennis-Refactoring-Kata) _

## Clean Code 🚀

_Características relacionadas en el código para visualizar diferentes ejemplos en donde se muestra como tener un clean code_

### Código enfocado 📋

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


## Entendible ⚙️

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

### Escalable🔩

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


### Duplicidad ⌨️
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

### Testeable⌨️
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

### Principio menor asombro⌨️

Nombres claros y precisos para métodos
```
public void wonPoint(String playerName) {

  public String getScore() {
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



