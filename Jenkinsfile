pipeline {
  agent {
    kubernetes {
      containerTemplate {
        name 'docker'
        image 'docker:1.11'
        ttyEnabled true
        command 'cat'
      }
    }
  }
  stages {
    stage('Run maven') {
        steps {
            container('docker') {
                withDockerRegistry(registry: [credentialsId: 'ContainerExecDecoratorPipelineTest-docker']) {
                    sh 'hostname'
                }
            }
        }
    }
  }
}


// pipeline {
//     agent {
//         docker {
//             image 'node:10-alpine' 
//             args '-p 3000:3000' 
//         }
//     }
//     environment {
//         CI = 'true'
//     }
//     stages {
//         stage('Build') { 
//             steps {
//                 sh 'npm install' 
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//         stage('Deliver') {
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//                 input message: 'Finished using the web site? (Click "Proceed" to continue)'
//                 sh './jenkins/scripts/kill.sh'
//             }
//         }
//     }
// }