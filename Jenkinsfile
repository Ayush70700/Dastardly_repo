pipeline {
    agent{
        label 'docker'
    }

    environment {

        DOCKER_IMAGE = 'public.ecr.aws/portswigger/dastardly:latest'

        WEBSITE_URL = 'https://testingxperts46-dev-ed.develop.my.salesforce.com/' // Change this to your target website URL

    }

    stages {

        stage('Build Docker Image') {

            steps {

                script {

                    // Build Docker image containing Dastardly

                    bat 'docker build -t $DOCKER_IMAGE', '-f C:\Program Files\Docker\Docker\resources\bin'

                }

            }

        }

        stage('Run Security Tests') {

            steps {

                script {

                    // Run Dastardly container based on the built image

                    bat "docker run --rm $DOCKER_IMAGE dastardly test $WEBSITE_URL"

                }

            }

        }

    }

}


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
