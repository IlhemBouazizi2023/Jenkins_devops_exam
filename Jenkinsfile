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
        environment
        {
        kubeconfig = credentials("config") // we retrieve  kubeconfig from secret file called config saved on jenkins
        }
      steps {
        script {
          def manifest = readFile('k3s/manifest_v1.yaml')
          
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