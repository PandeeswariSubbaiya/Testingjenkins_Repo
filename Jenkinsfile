pipeline {
    agent any
    tools { 
      maven 'maven3' 
      }
    environment{
      def mvnHome =  tool name: 'maven3', type: 'maven' 
      def BRANCH_NAME ='GIT_BRANCH'
  }
stages {
      stage('GIT checkout') {
                    steps {
                        script{
                               if (env.GIT_BRANCH.contains('main')) {
                            echo 'Hello from main branch'
                            git branch: 'main', url: 'https://github.com/PandeeswariSubbaiya/Sample.git'
                            }
                               else {
                                   echo "Run this stage only if the branch is not main"
                                  git branch: 'release', url: 'https://github.com/PandeeswariSubbaiya/Sample.git' 
                               }
                               }
                          }
                        }
    stage('Merge release to main') {
                        steps {
                            script {
                                sh "git checkout main"
                                sh "git merge --no-ff release"
                                    }
                                }
                             }
     stage('Push Changes') {
            steps {
                // Push changes to the Git repository
                withCredentials([usernamePassword(credentialsId: '<PandeeswariSubbaiya>', usernameVariable: 'PandeeswariSubbaiya', passwordVariable: 'Subbaiya@08')]) {
                    sh "git config user.name 'Pandeeswari'"
                    sh "git config user.email 'Pandeeswari318@gmail.com'"
                    sh "git push origin main"
                }
            }
        }
     }
  }
