pipeline {
  
  environment {
    dockerimagename = "adamhome/secondtest"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git branch: 'main', url: 'https://github.com/flyd0g/azure-jenkins-k8s-flask-hello-world.git'
      }
    }

    stage('Build Image') {
      steps {
        script {
          dockerImage = docker.build(dockerimagename)
        }
      }
    }

    stage('Push Image') {
      environment {
        registryCredential = 'dockerhub'
      }
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
            dockerImage.push("latest")
          }
        }
      }
    }
    
    stage('Deploy app to k8s') {
      steps {
        script {
          kubernetesDeploy configs: 'flask_app.yaml', kubeConfig: [path: ''], kubeconfigId: 'kubernetes', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
        }
      }
    }

  }
}
