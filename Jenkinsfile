pipeline {
  agent {
    kubernetes {
      yamlFile '.build-pod.yaml'  // path to the pod definition relative to the root of our project
    }
  }
  
  environment {
    PASSWORD="49494949466dfas9d4f9ase4gf9as4!fdsf#@#"
    
    DD_URL = "https://defectdojo.default.minikube.local"
    DD_API_KEY = credentials("DD_API_KEY")
    DD_PRODUCT_TYPE_NAME = "Neos Core"
    DD_PRODUCT_NAME = "Core Product"
    DD_SSL_VERIFY = "False"

    DD_TEST_NAME = "Gitleaks"
    DD_TEST_TYPE_NAME = "Gitleaks Scan"

    DD_ENGAGEMENT_NAME = """${sh(returnStdout: true, script: 'date --iso-8601=seconds')}"""

    DD_FILE_NAME = "reports/gitleaks.json"    
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
          sh 'gitleaks detect -s . -v -f json -r reports/gitleaks.json || true'
          sh 'cat reports/gitleaks.json'
          echo 'Deploy stage finished!'
        }
      }
    }
    
    stage("Upload reports"){
      steps{
        container("ddimport"){
          sh 'DD_FILE_NAME="reports/gitleaks.json"'
          sh 'dd-reimport-findings.sh'
        }
      }
    }
  }
}
