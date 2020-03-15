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
        sh "python --version" 
		}  
           }
         }
     }
  }
    
  

