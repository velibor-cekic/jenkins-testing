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
      }
    }
    stage("Deploy"){
      steps {
        echo 'Deploy step'
      }
    }
  }
}
