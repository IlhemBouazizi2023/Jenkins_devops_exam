pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        // Checkout your source code from version control
        // Replace the repository URL and credentials as needed
        checkout scm
      }
    }
    
    stage('Deploy to Kubernetes') {
      steps {
        script {
          def kubeconfig = readFile('~/.kube/config')
          def manifest = readFile('~/manifest_v1.yaml')
          
          // Configure Kubernetes CLI
          sh "echo '${kubeconfig}' > kubeconfig.yaml"
          withKubeConfig([credentialsId: 'config', file: 'kubeconfig.yaml']) {
            // Apply the manifest file to deploy Kubernetes resources
            sh "kubectl apply -f ${manifest}"
          }
        }
      }
    }
  }
}