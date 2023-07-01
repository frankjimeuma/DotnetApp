# Instrucciones para Aplicacion Dotnet

### Comandos a Ejecutar

| Fase | Comando |
| ------ | ------ |
| Dependencies | **dotnet restore** |
| Test | **dotnet test** |
| SonarScanner | **Revisar Seccion de SonarQube** |
| Build | **dotnet build** |
| Generate Artifacts | **dotnet publish -c Release** |
| Deploy | **sc stop DotnetAppService** |
| Deploy | **rmdir C:\deploy\DotnetApp\\ /s /q**   |
| Deploy | **xcopy bin\Release\net7.0\publish\\ C:\deploy\DotnetApp\\ /s /q /y** |
| Deploy | **sc start DotnetAppService** |

### Realizar cambios en la Aplicacion

La aplicacion va a mostrar un mensaje de bienvenida en Dotnet, para efectos del proyecto pueden cambiar el archivo que se ubica en `Pages\Index.cshtml` linea #8 

`<h1 class="display-4">Welcome</h1>`

Y agregar un texto despues del Welcome, ejemplo 

`<h1 class="display-4">Welcome from Romell Project</h1>`

### SonarQube Linux

```sh
stage('Run SonarQube'){
    steps{
        withSonarQubeEnv('SonarQubeCursoCI') {
            sh "/opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=DotnetApp"
        }
    }
}

stage('SonarQube Quality Gate') {
    steps {
        sleep 5
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}
```

### SonarQube Windows

```sh
stage('Run SonarQube'){
    steps{
        withSonarQubeEnv('SonarQubeCursoCI') {
            bat "sonar-scanner -Dsonar.projectKey=DotnetApp"
        }
    }
}

stage('SonarQube Quality Gate') {
    steps {
        sleep 5
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}
```
