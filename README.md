# PlantUML with Gradle
PlantUML example using Gradle to generate diagrams.

## Usage
Clone the repository and add PlantUML diagrams in the `src/diagram` directory, where you can already find some examples. The `src/config/design.puml` file contains an example how to create custom design file (colors, fonts, etc.), that is automatically applied to all of your diagrams.  

**Requires [Graphviz ](https://graphviz.org/) installation to use all features. Latest package can be downloaded from [Graphviz download page](https://graphviz.org/download/).** Further info can be found here: [PlantUML Getting Started](https://plantuml.com/starting)

Run: `gradlew clean build` (Windows) or `./gradlew clean build` (Linux)

The generated diagrams will be available in the `build` directory.

## Design customization
The example provides you a file that can be used for sharing style customization and variables (e.g.: for colors). You can find more information about this PlantUML feature here: [PlantUML skinparam](https://plantuml.com/skinparam)

To customize your design, update the `src/config/design.puml` file.

If you would like to use the default design, check the next section.

## Using default design
If you want to use the default PlantUML design or do not want to use a generic design file, you need to modify  the `build.gradle` file and remove `"-config", "$projectDir/src/config/design.puml"` from `args` parameter of the `plantUml` task.

Modify from this:
```
task plantUml(type: JavaExec) {
    group = "PlantUML"
    description = "Generate diagrams from PlantUML files."
    classpath configurations.plantUml
    main = "net.sourceforge.plantuml.Run"
    args "-config", "$projectDir/src/config/design.puml", "-o", "$buildDir", "$projectDir/src/diagram"
}
``` 

To this:
```
task plantUml(type: JavaExec) {
    group = "PlantUML"
    description = "Generate diagrams from PlantUML files."
    classpath configurations.plantUml
    main = "net.sourceforge.plantuml.Run"
    args "-o", "$buildDir", "$projectDir/src/diagram"
}
```

After this change you can remove the `src/config/design.puml` file.

## Not checking for Graphviz
Graphviz is not required if you only using sequence diagrams: [PlantUML without Graphviz](https://plantuml.com/smetana02)

If you would like to remove the check for Graphviz, remove or comment the following line from `build.gradle`:
```
tasks["plantUml"].dependsOn("plantUmlCheck")
```

Optionally you can also remove the following block:
```
task plantUmlCheck(type: JavaExec) {
    group = "PlantUML"
    description = "Check if GraphViz available for PlantUML."
    classpath configurations.plantUml
    main = "net.sourceforge.plantuml.Run"
    args "-testdot"
}
```
## Source
Example project cloned from: https://github.com/mracsko/plantuml
