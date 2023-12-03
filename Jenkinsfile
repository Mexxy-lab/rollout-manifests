node {
    def app
    
    env.IMAGE = 'pumejlab/bluegreen-rollout'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/Mexxy-lab/rollout-manifests.git'
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'pumej-gitpasswd', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        sh "git config user.email pumej1985@gmail.com"
                        sh "git config user.name Mexxy-lab"
                        //sh "git switch master"
                        sh "cat rollout.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' rollout.yml"
                        sh "cat rollout.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job Rolloutmanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/rollout-manifests.git HEAD:main"
             }
         }
     }
  }
}