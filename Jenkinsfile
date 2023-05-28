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
          sh 'ls'
          sh'gitleaks'
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
