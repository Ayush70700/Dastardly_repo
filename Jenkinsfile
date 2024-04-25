pipeline {
    agent any

    stages {
        stage('Prepare') {
            steps {
                script {
                    // Docker image for Dastardly
                    def dastardlyImage = 'public.ecr.aws/portswigger/dastardly:latest'
                    // Your target URL to scan
                    def targetUrl = 'https://testingxperts46-dev-ed.develop.my.salesforce.com/' 
                    // Path for the output report
                    def reportPath = 'dastardly-report.html'
                    
                    // Pull the Dastardly image from Docker Hub
                    bat "docker pull ${dastardlyImage}"
                }
            }
        }

        stage('Run Dastardly Scan') {
            steps {
                script {
                    // Run the Dastardly scan in Docker
                    // bat """
                    //     docker run \
                    //     --rm \
                    //     -v %cd%:/reports \
                    //     ${dastardlyImage} \
                    //     --config \"{\\\"targetURL\\\": \\\"${targetUrl}\\\"}\" \
                    //     --output-file \"/reports/${reportPath}\"
                    // """
                    bat "docker run --rm $DdastardlyImage dastardly test $targetUrl
                }
            }
        }

        stage('Archive Report') {
            steps {
                // Archive the report as a Jenkins artifact
                archiveArtifacts artifacts: 'dastardly-report.html', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Dastardly scan was successful.'
        }
        failure {
            echo 'Dastardly scan failed. Check logs for details.'
        }
    }
}







//2. pipeline {
//     // agent{
//     //     label 'docker'
//     // }
//     agent any
//     environment {

//         DOCKER_IMAGE = 'public.ecr.aws/portswigger/dastardly:latest'

//         WEBSITE_URL = 'https://testingxperts46-dev-ed.develop.my.salesforce.com/' // Change this to your target website URL
//         DOCKER_PATH = 'C:/Program Files/Docker/Docker/resources/bin'

//     }

//     stages {

//         stage('Build Docker Image') {

//             steps {

//                 script {

//                     // Build Docker image containing Dastardly

//                     // bat 'docker build -t $DOCKER_IMAGE -f $DOCKER_PATH'
//                     bat 'docker build -t public.ecr.aws/portswigger/dastardly:latest'

//                 }

//             }

//         }

//         stage('Run Security Tests') {

//             steps {

//                 script {

//                     // Run Dastardly container based on the built image

//                     bat "docker run --rm $DOCKER_IMAGE dastardly test $WEBSITE_URL"

//                 }

//             }

//         }

//     }

// }


// pipeline {
//   agent any
//   environment {
//     DASTARDLY_TARGET_URL='https://testingxperts46-dev-ed.develop.my.salesforce.com/'
//     IMAGE_WITH_TAG='public.ecr.aws/portswigger/dastardly:latest'
//     JUNIT_TEST_RESULTS_FILE='dastardly-report.xml'
//   }
//   stages {
//     stage ("Docker Pull Dastardly from Burp Suite container image") {
//       steps {
//         bat 'docker pull public.ecr.aws/portswigger/dastardly:latest'
//       }
//     }
//     stage ("Docker run Dastardly from Burp Suite Scan") {
//       steps {
//         //cleanWs()
//         bat '''
//           docker run --rm --user $(id -u) -v %WORKSPACE%:%WORKSPACE%:rw \
//           -e DASTARDLY_TARGET_URL=https://testingxperts46-dev-ed.develop.my.salesforce.com/ \
//           -e DASTARDLY_OUTPUT_FILE=%WORKSPACE%/dastardly-report.xml \
//           public.ecr.aws/portswigger/dastardly:latest
//         '''
//       }
//     }
// }
//   post {
//     always {
//       junit testResults: "${JUNIT_TEST_RESULTS_FILE}", skipPublishingChecks: true
//     }
//   }
// }


// pipeline {
//   agent any
//   environment {
//     DASTARDLY_TARGET_URL='https://testingxperts46-dev-ed.develop.my.salesforce.com/'
//     IMAGE_WITH_TAG='public.ecr.aws/portswigger/dastardly:latest'
//     JUNIT_TEST_RESULTS_FILE='dastardly-report.xml'
//   }
//   stages {
//     stage ("Docker Pull Dastardly from Burp Suite container image") {
//       steps {
//         sh 'docker pull ${IMAGE_WITH_TAG}'
//       }
//     }
//     stage ("Docker run Dastardly from Burp Suite Scan") {
//       steps {
//         //cleanWs()
//         sh '''
//           docker run --rm --user $(id -u) -v ${WORKSPACE}:${WORKSPACE}:rw \
//           -e DASTARDLY_TARGET_URL=${DASTARDLY_TARGET_URL} \
//           -e DASTARDLY_OUTPUT_FILE=${WORKSPACE}/${JUNIT_TEST_RESULTS_FILE} \
//           ${IMAGE_WITH_TAG}
//         '''
//       }
//     }
//   }
//   post {
//     always {
//       junit testResults: "${JUNIT_TEST_RESULTS_FILE}", skipPublishingChecks: true
//     }
//   }
// }
