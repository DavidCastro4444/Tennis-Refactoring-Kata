# Tennis Refactoring Kata

_Este proyecto es el resultado de aplicar técnicas de Refactoring y Code Smell, el proyecto raiz que se utilizo como base dle ejercício se puede encontrar en este [Repositorio](https://github.com/emilybache/Tennis-Refactoring-Kata) _

## Para Empezar 🚀

_El proyecto propuesto otorga diferentes clases que permiten indagar en técnicas de Refacotoring para tratar aplicar al mismo proyecto_t


### Pre-Requisitos 📋

_El proyecto corre bajo la versión java 8 mínimo para su compilación_

## Ejecutando las pruebas ⚙️

_El proyecto contiene una clase llamada TennisTest.java en donde se valida que su funcionamiento es el esperado_

La forma para correr la prueba unitaria se aconseja que sea por consola 

```
mvn test
```

### Analice las pruebas end-to-end 🔩

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


### Técnicas Clase TennisGame1⌨️
_Code smells_

Decompose Conditional en las líneas 26 a 71

Replace Conditional with Polymorphism

Remove Assignments to Parameters


### Técnicas Clase TennisGame2⌨️
_Code smells_

Consolidate Duplicate Conditional Fragments en las líneas 18 a 99

Decompose Conditional en las líneas 26 a 71

Replace Conditional with Polymorphism

Remove Assignments to Parameters

### Técnicas Clase TennisGame3⌨️

_Code smells_

Extract Variable

### Técnicas Clase TennisGame4⌨️

_Code smells_

Extract Variable


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


