pipeline {
    agent {
	label 'windows-agent'
	}   
    

    //Declaracion de valores de entorno
    environment {
        MESSAGE = "Curso de Intgracion Continua"
        LISTA_CORREOS = "franklin.jimenezumana@ucreativa"
        CUERPO_CORREO = "El pipeline ${BUILD_URL} tuvo un resultado"
        TITULO_CORREO = "${BUILD_URL} STATUS"
        AWS_ACCESS_KEY_ID=credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY=credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION='us-east-1'
    }


  
    stages {
        stage('Bienvenida!') {
            steps {
                echo "Bienvenid@s al ${MESSAGE}, estamos corriendo en ${BUILD_URL} y este es el build ${BUILD_NUMBER} , also this is the node with name ${NODE_NAME} and Workspace ${WORKSPACE} in Jenkins location ${JENKINS_URL}"
            }
        }

	  stage('cambio sugerido') {
            steps {
                bat 'echo hola'
            }
        }

	    
        stage('Instalar dependencias') {
            steps {
                bat 'dotnet restore'
            }
        }
      
        stage('Correr pruebas de unidad') {
            steps {
                bat 'dotnet test'
            }
        }  

	stage('Run SonarQube'){
    	     steps{
        	withSonarQubeEnv('SonarQubeCursoCI') {
            	bat "sonar-scanner -Dsonar.projectKey=DotnetApp"
                   } 
            }
        }
       
        stage('Compilacion de la aplicacion Dotnet') {
            steps {
                bat 'dotnet build'
            }
        }
        

        stage('Generar Artifacts') {
            steps {
                bat 'dotnet publish -c Release'
            }
        }

	stage('Deploy') {
            steps {
                bat 'sc stop DotnetAppService'
		bat 'rmdir C:\\deploy\\DotnetApp\\ /s /q'
		bat 'xcopy bin\\Release\\net7.0\\publish\\ C:\\deploy\\DotnetApp\\ /s /q /y'
		bat 'sc start DotnetAppService'
            }
        }
        
        stage('success') {
            steps {
                bat 'dir'
              
        
            }
        }
    }

      
    post {
      always {
          echo 'siempre me voy a ejecutar...no matter what happens in the world :| '
      }
      success {
          emailext body: "${CUERPO_CORREO} exitoso", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
      }
      failure {
          emailext body: "${CUERPO_CORREO} fallido", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
      }
 //     success {
   //       echo 'El ipeline da ok :)'
     // }
      //failure {
        //  echo 'Algo Salio Mal :('
      //}
    
    }


      
    
}
