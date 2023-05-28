pipeline {
  agent {
    kubernetes {
      yamlFile '.build-pod.yaml'  // path to the pod definition relative to the root of our project
    }
  }
  
  environment {
    PASSWORD="49494949466dfas9d4f9ase4gf9as4!fdsf#@#"
  }
  
  stages {
    stage("Build"){
      steps{
          echo 'Build step! Simple creation of reports directory'
          sh 'mkdir reports'
          sh 'env'
          echo 'Build step finished!'
          
      }
    }
    stage("Deploy"){
      steps {
        container('gitleaks'){
          echo 'Executing in gitleaks container'
          sh 'ls'
          sh 'gitleaks detect -s . -v -f json -r reports/gitleaks.json'
          sh 'cat reports/gitleaks.json'
          echo 'Deploy stage finished!'
        }
      }
    }
    
    stage("Upload reports"){
      steps{
        container("ddimport"){
          sh 'dd-import-languages.sh'
      }
  }
}
