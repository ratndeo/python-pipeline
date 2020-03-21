properties([parameters([string(defaultValue: '', description: '', name: 'tenant', trim: true), string(defaultValue: '', description: '', name: 'tenantEnv', trim: true)])])
pipeline {
  agent {
    kubernetes {
      label 'python_slave'  // all your pods will be named with this prefix, followed by a unique id
      yamlFile 'build-pod.yaml'  // path to the pod definition relative to the root of our project 
      instanceCap 3
    }
  }
  stages {
    stage('Build') {
      steps {  // no container directive is needed as the maven container is the default
      container('python') {
        echo "tenant is : ${params.tenant}"
        echo "tenantEnv is : ${params.tenantEnv}"
        echo "python version is"
        sh "python --version" 
        sh "python hello.py" 
		}  
           }
         }
     }
	post {
		always {
			archiveArtifacts artifacts: 'pythonArchieve.txt', onlyIfSuccessful: true
			emailext attachLog: true, body: "${env.PROJECT_NAME} - Build # ${env.BUILD_NUMBER} - ${env.BUILD_STATUS}:\nCheck console output at ${env.BUILD_URL} to view the results.", compressLog: true, subject: "${env.PROJECT_NAME} - Build # ${env.BUILD_NUMBER} - ${env.BUILD_STATUS}!", to: 'ratna.deo@lendfoundry.com'
			//emailext attachLog: true, compressLog: true,  to: 'ratna.deo@lendfoundry.com'
		}
	}
	
  }
    
  

