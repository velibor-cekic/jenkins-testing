pipeline {
  agent {
    kubernetes {
      yamlFile '.build-pod.yaml'  // path to the pod definition relative to the root of our project
    }
  }
  
  stages {
    stage("Build"){
      steps{
          echo 'Build step'
          sh 'hostname'
          sh 'pwd'
          echo 'Finished steps in build stage!'
      }
    }
    stage("Deploy"){
      steps {
        echo 'Deploy step'
      }
    }
  }
}
