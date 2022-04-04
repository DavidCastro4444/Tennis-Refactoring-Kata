# Architectural Debt

A lo largo del proyecto se han identificado diferentes escenarios que abarcan fuentes de deuda técnica, estas facetas de un
proyecto de software muestran los diferentes obstaculos que debemos afrontar para decir con mayor seguridad que es un producuo 
de alta calidad.

En esta face nos vamos a centrar en la arquitectura, acá nos vamos a referir a architectural smells, teniendo como foco central
problemas estructurales en los componentes como podría software de grups de classes y su interacción con otros componentes. ejemplos de este smell
se tienen como:  componente dios y estructuras densas. Encontrar estos errores de diseño de arquitectura son escensiales e indispensables
dado que la no actuación a tiempo, correspondería a elevados costos de arreglo a las malas decisiones tomadas.


## Características 📑

Durante la última decada se han desarrollado diferentes técnicas para capturar malas decisiones al momento de desarrollar una arquitectora en el proyecto 
que se encuentra esarrollo, pero para entender la importancia de realizar estos procesos; hace falta identificar el impacto que genera estas malas decisiones 
en el resultado del proyecto. Estas son algunas consecuencias directas architectura

✔️ Mantenibilidad de los sistemas web

✔️ Rendimiento del software

✔️ Aplicaciones redundantes.

✔️ Tecnología obsoleta

✔️ Re-keying manual

✔️ Data redundante

✔️ Soluciones alternativas, rápidas y torpes

✔️ Erosión de la arquitectura del software

### Ejemplos 📋

![image](https://user-images.githubusercontent.com/26014448/161473384-e3045cbb-62b1-4b9b-b475-4960bb5aab38.png)

✔️ Definiciones iniciales no modulares

✔️ Extrema complejidad

✔️ No cumplimiento de drivers de negocio

✔️ Diseños no actualizados o no existentes

✔️ Frameworks o lenguajes no adecuados

 
## Tipos de Architecture Smells ⚙️
![image](https://user-images.githubusercontent.com/26014448/161473794-c854014a-2bd9-4945-9151-5f30dac8142a.png)

### Metodologías para la recoleccion de errores 🔩

_Dado que existen formas muy diversas en la aparición smell, se sugiere las siguientes formas de identificación de errores_

✔️ Preguntas sobre salud del sistema / Esto permite entender malestares y errores en las áreas afectadas, se debe partir de un error intrínsico proveniente del sesgo de 
los involucrados, y se debe proceder con objetividad para la recoleccion de información y tramiento de la misma.

✔️ Analizar código para encontrar hallazgos relacionados / El código es nuestra primera herramienta para preveer anti patrones y reconocer escenarios de mal olor en la rquitectura. 
Aquí se puede ver mala abstración de procesos, lógica redundante o capas faltantes en el proceso de desarrollo

✔️ Analizar drivers y restricciones de arquitectura / Los drivers de la arquitectura incluyen principalmente a los atributos de calidad. Además de esto, incluyen a un 
subconjunto de los casos de uso que se consideran como primarios. Los casos de uso primarios son aquellos de mayor importancia o de mayor complejidad para el negocio. 
Por último, las restricciones también son consideradas como drivers arquitecturales.

✔️ Examinar arquitectura / 


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
