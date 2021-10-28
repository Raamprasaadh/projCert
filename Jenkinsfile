pipeline { 

environment { 

	registry = "raamprasasdh/demo" 

	registryCredential = 'DockerHubpwd@1' 

	dockerImage = '' 

}

agent any 

stages { 

	stage('Cloning our Git') { 

		steps { 

			git 'https://github.com/Raamprasaadh/projCert.git' 

		}

	} 

	stage('Building our image') { 

		steps { 

			script { 

				dockerImage = docker.build registry + ":$BUILD_NUMBER" 

			}

		} 

	}

	stage('Push our image') { 
		steps { 

			script { 

				docker.withRegistry( '', registryCredential ) { 

					dockerImage.push() 

				}

			} 

		}

	} 


    stage ('Deploy to Conatiner') {
     steps {
         echo "Run containers" + dockerImage
         script {
          sh "docker run -d -p 8081:80 $registry:$BUILD_NUMBER"
                     }
                  }
  } 
  
/*
	stage('Cleaning up') { 
		steps { 
			sh "docker rmi $registry:$BUILD_NUMBER" 
		}
	} 
*/

}

}
