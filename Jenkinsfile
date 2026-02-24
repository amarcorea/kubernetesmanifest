node('docker-executor') {

    String USER_GITHUB = "amarco.rea@gmail.com"
    String NAME_GITHUB = "Marco Rea"
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'githubcreds', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email ${USER_GITHUB}"
                        sh "git config user.name ${NAME_GITHUB}"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+${DOCKERIMAGE}.*+${DOCKERIMAGE}:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job ${env.JOB_NAME}: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
