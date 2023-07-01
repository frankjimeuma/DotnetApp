# Instrucciones para Aplicacion Dotnet

### Agente 
El agente para ejecutar la app Dotnet tiene por etiqueta `windows-agent`

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

### SonarQube Windows

### SonarQube Windows

```sh
stage('Run SonarQube'){
    steps{
        withSonarQubeEnv('SonarQubeCursoCI') {
            bat "sonar-scanner -Dsonar.projectKey=DotnetApp"
        }
    }
}
```

### Visualizacion de la Aplicacion
La aplicacion se puede acceder por medio del URL: 

`http://ucreativa-agent.eastus.cloudapp.azure.com:5000/`
