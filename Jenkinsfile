pipeline {
    environment {
        registry = "docreg.eprocure.gov.pk:5000/test"
        dockerImage = ""
    }
    agent any
    stages {
        stage('git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/faheemkhan5/test.git'
            }
        }
        stage('docker build and push') {
            steps{
              script {
                 dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
            }
        }
        stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push("${BUILD_NUMBER}")
          }
        }
      }
        }
        stage('Trigger Update dockertag') {
       steps{
            echo "triggering updatemanifestjob"
            build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.":$BUILD_NUMBER")]
        }
        }
    }
}
