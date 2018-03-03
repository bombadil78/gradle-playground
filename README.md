# Gradle
Gradle is a flexible build system similar to Maven. Tasks are configured in Groovy. There exist plenty of plugins for different project types.

The most important configuration files are:
* build.gradle: Build-Configuration; defines dependencies, plugins used an
* settings.gradle

Gradle offers task extension based on built-in gradle tasks or introduction of custom tasks.

## Wrapper
Since also the build system used to build a project is evolving there exists a wrapper. A wrapper is generated using the following gradle command:

```bash
gradle wrapper
```

This will generate the following files:
* *gradlew* and *gradlew.bat*: Scripts to run the wrapper
* *gradle* folder, which contains the following files
  * *gradle-wrapper.jar*: The wrapper executable
  * *gradle-wrapper.properties*: The wrapper configuration file
  
The gradle wrapper will not run commands, but delegate to the configured version of gradle in order to perform the build task. The wrapper will lookup whether the corresponding version exists locally; if it is missing it will be downloaded before any tasks are executed.
 
The relevant gradle version in order to build the project as well as the folder to search for gradle versions is configured in the properties file. On Linux the versions are saved in ~/gradle/wrapper/dists.

All files generated by the gradle wrapper have to be added to version control.

## Basics
The *build.gradle* is the build configuration files. Tasks are the most basic steps of the build process.

Definition of a task
```bash
task one {
  println 'task one'
}

task one {
  doFirst {
    println 'done before task'
  }
}

task one {
  doLast {
    println 'done after task'
  }
}    

task one << {
  println 'similar to doLast'
}

```
Express task dependencies
```bash
// option #1
task one {}
task two (dependsOn: one) {}

// option #2
task A {}
task B {}
task C {}
C.dependsOn A, B
````

Definition of default tasks
```bash
defaultTasks 'foo', 'bar'
````

Use closure to define tasks 
```bash
task myTask {}

myTask {
    someProp = 'myValue'
    ...
}
````

Use closure to define task dependencies
```bash
task X {}
X.dependsOn {
    'Y'
}
````

Other features are:
* Enabling / disabling of tasks based on conditions, e.g. command-line arguments, ...
* Definition of inputs and outputs of a task to get a notion of up-to-date; implemented by taking snapshots of directories and comparing hash values.

## Implementation
Gradle creates a DAG of all the task dependencies **before** anything is executed.

There are three phases in the build process:
* Initialization
* Configuration 
* Execution

During initialization the settings.gradle file is executed. This file is mandatory for multi-project builds. One can use it to declare the set of subprojects or other global stuff.

If no setting.gradle file is found then gradle searches for it either in a master sibling directory or in the parent directory in order to build the project as part of a multi-project build. This behavior can be suppressed using the -u option.

There exist various lifecycle hooks in order to add additional steps to the build process. Possible hooks are:
* Before / after project evaluation
* Before / after task is added
* ...

## Multi-project builds
Projects are configured using *build.gradle* configuration files. Every project can optionally have a build configuration file. It is possible to configure any project from any build configuration file using *project()* as long as they are part of a multi-project build. This is called *cross-project configuration*. In order to create multi-project builds subproject relations must be expressed using *include* or *includeFlat* in the settings file of a parent project.

There are three relevant phases in a Gradle Build:
* Initialization: Creation of a *Project* representation for all relevant participating projects of the build
* Configuration: Configuration of the participating projects; takes into account configuration dependencies
* Execution: Execution of the participating projects; takes into account execution dependencies

A multi-project build is expressed through a dedicated *master* sibling directory or a parent directory containing a *settings.gradle* file where subproject relations are expressed using *includeFlat* or *include*.

Configuration abstraction can be expressed in the root project using the following approaches:
* *allprojects*: Configuration common to all projects
* *subprojects*: Configuration common to all subprojects
* *project(somePath)*: Configuration for a given project
* *configure(subprojects.findAll(...)*: Configuration common to a set of projects

### Execution dependencies
Tasks are executed using two different approaches:
* Explicitly using column notation, e.g. ./gradlew :p1:hello :p2:goodbye
* Implicitly using only the task name, e.g. ./gradlew hello 

There are two ways to express execution dependencies:
* Top-down: A 

# Questions
* 


### Plugin java-application
* java-application plugin as an example:
  * what are the assumptions?
  * how is it connected to gradle init?
  * describe tasks
    * clean
    * build
    * javadoc
    * 
    
### Plugin org.springframework.boot
* what is there more in addition?

### Plugin idea
* what is it?    

## Initialization
By default only the wrapper and init task is added to gradle, among with some helper tasks like depenceny graph or task viewer.

The init task can be used to bootstrap a new project by adding relevant build tasks, directory layouts, dependencies, ...

Supported types:
* ...
