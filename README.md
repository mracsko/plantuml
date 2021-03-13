# PlantUML with Gradle
PlantUML example using Gradle to generate diagrams.

## Usage
Clone the repository and add PlantUML diagrams in the `src/diagram` directory.

There are some example diagrams and design in the repository:

- `src/diagram` directory contains some test diagrams
- `src/config/design.puml` file contains an example how to create custom design file (colors, fonts, etc.), that is automatically applied to all of your diagrams

Run: `gradlew clean build` (Windows) or `./gradlew clean build` (Linux)

The generated diagrams will be available in the `build` directory.

## Design customization
The example provides you a file that can be used for sharing style customization and variables (e.g.: for colors). You can find more information about this PlantUML feature here: [PlantUML skinparam](https://plantuml.com/skinparam)

To customize your design, update `src/config/design.puml` file.

If you would like to use the default design, check the next section.

## Using default design
If you want to use the default PlantUML design or do not want to use a generic design file, you need to modify  the `build.gradle` file and remove `"-config", "$projectDir/src/config/design.puml"` from `args` parameter of the `plantUml` task.

Modify from:
```
task plantUml(type: JavaExec) {
    ...
    args "-config", "$projectDir/src/config/design.puml", "-o", "$buildDir", "$projectDir/src/diagram"
	...
}
``` 

To:
```
task plantUml(type: JavaExec) {
    ...
    args "-o", "$buildDir", "$projectDir/src/diagram"
	...
}
```