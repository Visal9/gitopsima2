node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email ima@gmail.com"
                        sh "git config user.name Imantha"
                        sh "git switch main"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+imantha95/doc.*+imantha95/doc:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh  "git pull"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/gitopsima.git HEAD:main"
      }
    }
  }
}
}
