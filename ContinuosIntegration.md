# Continuos Integration

La integración continua (CI) es una práctica de software que requiere enviar código con frecuencia a un repositorio compartido. Confirmar código con mayor frecuencia detecta errores antes y reduce la cantidad de código que un desarrollador necesita depurar para encontrar el origen de un error. Las actualizaciones frecuentes de código también facilitan la combinación de cambios de diferentes miembros de un equipo de desarrollo de software. Esto es excelente para los desarrolladores, que pueden pasar más tiempo escribiendo código y menos tiempo depurando errores o resolviendo conflictos de fusión.

Cuando confirma código en su repositorio, puede compilar y probar continuamente el código para asegurarse de que la confirmación no introduzca errores. Sus pruebas pueden incluir filtros de código (que verifican el formato de estilo), controles de seguridad, cobertura de código, pruebas funcionales y otros controles personalizados.

Construir y probar su código requiere un servidor. Puede compilar y probar actualizaciones localmente antes de enviar el código a un repositorio, o puede usar un servidor de CI que verifica las nuevas confirmaciones de código en un repositorio.

## CI usando GitHub Actions 🚀

CI usando GitHub Actions ofrece flujos de trabajo que pueden construir el código en su repositorio y ejecutar sus pruebas. Los flujos de trabajo pueden ejecutarse en máquinas virtuales alojadas en GitHub o en máquinas que usted mismo aloja.

Puede configurar su flujo de trabajo de CI para que se ejecute cuando se produzca un evento de GitHub (por ejemplo, cuando se inserte código nuevo en su repositorio), en un horario establecido o cuando se produzca un evento externo mediante el webhook de distribución del repositorio.

GitHub ejecuta sus pruebas de CI y proporciona los resultados de cada prueba en la solicitud de extracción, para que pueda ver si el cambio en su rama introduce un error. Cuando todas las pruebas de CI en un flujo de trabajo pasan, los cambios que impulsó están listos para ser revisados por un miembro del equipo o combinados. Cuando falla una prueba, uno de sus cambios puede haber causado la falla.

###  File YAML📋
Los archivos de flujo de trabajo utilizan la sintaxis YAML y deben tener una extensión de archivo .ymlo .yaml
Debe almacenar archivos de flujo de trabajo en el .github/workflowsdirectorio de su repositorio.

## name ⚙️

El nombre de su flujo de trabajo. GitHub muestra los nombres de sus flujos de trabajo en la página de acciones de su repositorio. Si omite name, GitHub lo establece en la ruta del archivo de flujo de trabajo en relación con la raíz del repositorio.

La forma para correr la prueba unitaria se aconseja que sea por consola 

```
name: Build
```

### On 🔩

Para desencadenar automáticamente un flujo de trabajo, use onpara definir qué eventos pueden hacer que se ejecute el flujo de trabajo.

Puede definir eventos únicos o múltiples que pueden desencadenar un flujo de trabajo o establecer un cronograma. También puede restringir la ejecución de un flujo de trabajo para que solo se produzca en archivos, etiquetas o cambios de rama específicos. 

```
name: Build
on:
```

### Filtros⌨️

Algunos eventos tienen filtros que le brindan más control sobre cuándo debe ejecutarse su flujo de trabajo.

Por ejemplo, el pushevento tiene un branchesfiltro que hace que su flujo de trabajo se ejecute solo cuando se produce una inserción en una rama que coincide con el branchesfiltro, en lugar de cuando se produce cualquier inserción.

```
name: Build
on:
  push:
    branches:
      - main
```

### on.<pull_request|pull_request_target>.<branches|branches-ignore>⌨️ 

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
### Jobs⌨️
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
### Build⌨️

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
### Análisis de código⌨️

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

### Pruebas⌨️

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



