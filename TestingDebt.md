# Testin Debt

Para establecer una afirmación objetiva de código de calidad en nuestro proyecto, es fundamental entender el concepto de deuda técnica por Testing, estableciendo como base,
más no única y ni aseverando que se haga de  forma completa, las pruebas unitarias. Siendo tan importante la claridad y calidad de nuestro código, existen diferentes patrones 
para la creación y seguimiento de nuestro código, algunos de ellos relacionados con metodologías ágiles como se evidencia en esta [página](https://biblioteca.sistedes.es/wp-content/uploads/2016/08/CEDI_2016_paper_139.pdf)

Para este proyecto contamos con una clase de Test, que permite realizar y validar el comportamiento esperado de las diferentes clases utilizadas y 
diseñadas en el proyecto. A continuación se hara un análisis de la intención, calidad y relevancia de la prueba unitara.

## Características 📑

No existe una definición única que restrinja el diseño de las pruebas unitarias, sin embargo, existen unos principios aceptados de forma generalizada que establecen unos objetivos a cumplir al momento de pretender crear una prueba. Estos principios se conocen como F.I.R.ST. 

✔️ Fast: Su ciclo de vida debe ser corto, tiempo esperado no superior a 5 segundos.

✔️ Isolated: Su ciclo de vida no debe verse afectado por el funcionamiento o comportamiento de ninguna prueba externa o recurso.

✔️ Repeatable: Debe repetirse de manera indefinida y no verse afectado su comportamiento por eso.

✔️ Self Validation: Debe ser auto evaluable, esto quiere decir que la prueba misma representa el resultado y no genera ambigüedad para entenderlo, haciendo que sea false o true.

✔️ Timely: Va relacionado con el ciclo del proyecto, esta característica va relacionada con lo oportuno de la prueba, haciendo hincapié en la creación de pruebas antes de salir a producción como valor mínimo esperado.


### Estándares de nombramiento 📋

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


## Concejos ⚙️

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

### Malas prácticas🔩

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


### Pruebas faltantes ⌨️
_Se debe hacer prueba por los 2 métodos de la interfaz usada, evidenciandose a continuación_
```
 public interface TennisGame {
    void wonPoint(String playerName);
    String getScore();
}
```

### Coverage ⌨️
_Dado que faltan componentes por probar, se evidencia un coverage del 70%_

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
