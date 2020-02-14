/**
 * This pipeline executes Selenium tests against Chrome and Firefox, all running in the same Pod but in separate containers
 * and in parallel
 */

pipeline {
  agent {
    kubernetes {
      yamlFile 'kubernetespod.yaml'
    }
  }
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/carlossg/selenium-example.git'
        parallel (
          firefox: {
            container('maven-firefox') {
              stage('Test firefox') {
                sh 'mvn -B clean test -Dselenium.browser=firefox -Dsurefire.rerunFailingTestsCount=5 -Dsleep=0'
              }
            }
          },
          chrome: {
            container('maven-chrome') {
              stage('Test chrome') {
                sh 'mvn -B clean test -Dselenium.browser=chrome -Dsurefire.rerunFailingTestsCount=5 -Dsleep=0'
              }
            }
          }
        )
      }
    }

    // stage('Logs') {
    //   containerLog('selenium-chrome')
    //   containerLog('selenium-firefox')
    // }
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