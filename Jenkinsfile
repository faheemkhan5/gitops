node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github02', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email fazalerahim2@gmail.com"
                        sh "git config user.name faheemkhan5"
                        //sh "git switch master"
                        sh "cat website.yaml"
                        sh "sed -i 's+docreg.eprocure.gov.pk/test.*+docreg.eprocure.gov.pk/test:${DOCKERTAG}+g' website.yaml"
                        sh "cat website.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/gitops.git HEAD:main"
       }
     }
   }
 }
}
