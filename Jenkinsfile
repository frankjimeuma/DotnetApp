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
      
        stage('Instalar dependencias') {
            steps {
                sh 'npm install'
                //sh 'curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"'
                //sh 'unzip awscliv2.zip'
                //sh 'sudo ./aws/install'
            }
        }
      
        //stage('Correr pruebas de unidad') {
           // steps {
                //sh 'npm run test'
            //}
        //}  
      
        stage('Compilacion de la aplicacion Angular') {
            steps {
                sh 'npm run build'
            }
        }
        

        stage('Mostrar Archivos') {
            steps {
                sh 'ls dist'
            }
        }
        
        stage('success') {
            steps {
                sh 'ls -la'
              
        
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
