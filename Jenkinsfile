node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
      script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              withCredentials([usernamePassword(credentialsId: 'github-username-token', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                  sh "cat deployment.yaml"
                  sh "sed -i 's+tylerpitcher/test.*+tylerpitcher/test:${DOCKERTAG}+g' deployment.yaml"
                  sh "echo ----------------------------------------------"
                  sh "cat deployment.yaml"
                  sh "git config --global user.name ${USERNAME}"
                  sh "git commit -am 'Updated version number'"
                  sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${USERNAME}/kubernetes-manifest.git"
      }
    }
  }
}
}
