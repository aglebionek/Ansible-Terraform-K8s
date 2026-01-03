# MAVEN is a Java build tool, that also manages dependencies.

## Resources
- [Maven](https://maven.apache.org/)
- [Maven Repository](https://mvnrepository.com/)


## Installation
### Linux
```bash
sudo apt update && sudo apt install maven
```
### Windows
1. Download the latest version of Maven from [here](https://maven.apache.org/download.cgi).
2. Extract the archive to a folder.
3. Add the bin directory to the PATH environment variable.
4. Verify the installation by running `mvn -version`.


## Commands
Create a new project in non-interactive mode
```bash
mvn archetype:generate -DgroupId=<package_name, like 'com.mycompany.app'> -DartifactId=<name_of_the_project, like 'my-app'> -DinteractiveMode=false -DarchetypeVersion=<version, like '0.1'> -DarchetypeArtifactId=<artifact_id, like 'maven-archetype-quickstart'> -DarchetypeGroupId=<group_id, like 'org.apache.maven.archetypes'>
```
Or to run in interactive mode
```bash
mvn archetype:generate 
```

