# MDE4CPP
**Welcome to MDE4CPP project**

## Content
Further information can be found on [project site] (http://sse.tu-ilmenau.de/mde4cpp)

## Installation instructions
1. Install following software:
  * Java Development Kit (JDK) version 1.8
  * Eclipse Modeling Tool
    * add plugin Acceleo 3.7 for Eclipse Oxygen (use Acceleo 3.6 for older Eclipse versions)
  * Gradle 4.5.1 or older
	* Go to ${user folder}/.gradle 
	* create file gradle.properties
		* create entry: make_parallel_jobs=number
		* number ... count of parallel build jobs
  * MinGW:
	* for building 32 bit applications: (choose one)
		* [MinGW](http://www.mingw.org/) with packages mingw32-gcc-g++, mingw32-make, mingw32-libpthreadgc (If you want to use prebuilt libraries, you have to use the version MinGW.org GCC-6.3.0-1.)
		* [mingw-w64](https://mingw-w64.org/doku.php), select architecture = i686 during installation
	* for building 64 bit applications:
		* [mingw-w64](https://mingw-w64.org/doku.php), select architecture = x86_64 during installation
  * CMake
  	
2. checkout a repository with one of the following options:
  * clone [MDE4CPP] (https://github.com/MDE4CPP/MDE4CPP) respository and update submodules
  * clone one or more subrepositories of MDE4CPP according to your requirements
  
3. Open Advanced System Settings
  * modify system environment variable PATH: add CMake bin folder, Gradle bin folder and MinGW bin folder
    * create environment variable `MDE4CPP_ECLIPSE_HOME` with path to root folder of Eclipse modeling Tool
  * create environment variable `MDE4CPP_HOME` with path to MDE4CPP root folder
	  (Please note, that the root folder include the subfolder "application" with 
    * binaries inside `${MDE4CPP_HOME}/application/bin` and 
    * header files inside `${MDE4CPP_HOME}/application/include/{model name}`.)

4. If you want to use Prebuild libraries, packages are downloadable on github. Package with all libraries and header files are available at MDE4CPP repository. All C++ libraries are avaiable in
  * debug version (compiler flag -ggdb)
  * release version (mostly with compiler flag O3, no debug messages).
Unpack downloaded packages into `${MDE4CPP_HOME}/application`.

5. If you want to build by yourself, be familar with gradle. Some basics are described below. Basic gradle tasks:
  * `gradle tasks` ... list of available tasks is available.
  * `gradle projects` ... package overview is available
  * `gradle help` ... gradle help
  * `gradle <task name>` ... run task <task name>

6. List of top level tasks (MDE4CPP tasks):
  * `buildAll` ... create executables of all generators and build all base models
  * use `gradle tasks` to find all top level commands under `MDE4CPP tasks`
  * generator tasks:
    * `createAllGenerators` ... create executables of all generators
    * `create<Generator project name>` ... creates executable of corresponding generator, e.g. createUML4CPP
  * examples can be found in [example](https://github.com/MDE4CPP/examples) or after cloning the repositories in src/examples. Collection of examples can be build with task *buildAllExamples* (most projects are includes).

7. Model tasks are names using following schema: `<command><modelName> <buildMode>`
  * commands:
    * `build` ... execute commands generate and compile
    * `generate` ... generate C++ code using our generator (independent of build mode)
    * `compile` ... compile generated files
  * `modelName` ... name of the model, starting with capital letter
  * `buildMode`
    * not specified ... build debug and release version
    * `-PDEBUG` or `-PD` ... debug version -> compiler flags -g -ggdb is used
    * `-PRELEASE` or `-PR` ... release version -> mostly with compiler flag O3, debug messages are disabled
	* The build mode can be preconfigured in file ${user folder}/.gradle/gradle.properties by adding
		* DEBUG or D ... build debug version 
		* RELEASE or R ... build release version
		* This build mode is always used when compiling.
	* A build mode can be disabled by setting the value `0`. For instance, the debug version is not built if `-PDEBUG=0` is defined in a gradle command.
	* Further information for configuration and execution of compile tasks can be found on [MDE4CPPCompile-Plugin](https://github.com/MDE4CPP/MDE4CPPGradlePlugins).
  * examples:
	* no preconfigured build mode inside gradle.properies: 
		* `buildEcore` - generate and compile ecore.ecore in debug and release
		* `generateEcore` - generate C++ code for ecore.ecore
		* `compileEcore -PRELEASE` - compile generated code of ecore.ecore in release version
	* gradle.properies includes DEBUG	
		* `buildEcore` - generate and compile ecore.ecore in debug
		* `generateEcore` - generate C++ code for ecore.ecore
		* `compileEcore -PRELEASE` - compile generated code of ecore.ecore in release and debug version
		* `compileEcore -PRELEASE -PDEBUG=0` - compile generated code of ecore.ecore in release version (debug is disabled)

  All binaries and header files are delivered to `${MDE4CPP_HOME}/application` using the tasks. 