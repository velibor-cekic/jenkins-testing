pipeline {
  agent {
    kubernetes {
      yamlFile '.build-pod.yaml'  // path to the pod definition relative to the root of our project
    }
  }
  
  stages {
    stage("Build"){
      steps{
          echo 'Build step! Simple creation of reports directory'
          sh 'mkdir reports'
          echo 'Build step finished!'
          
      }
    }
    stage("Deploy"){
      steps {
        container('gitleaks'){
          echo 'Executing in gitleaks container'
          sh 'gitleaks detect -s . -v -f json -r reports/gitleaks.json'
          sh 'cat reports/gitleaks.json'
          echo 'Deploy stage finished!'
        }
      }
    }
  }
}
