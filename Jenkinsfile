pipeline {
     agent any
     stages {
         stage('Build') {
              steps {
                  sh 'echo Building...'
              }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
         stage('Build Docker Image') {
              steps {
                  sh 'docker build -t capstone-app .'
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh "docker tag capstone-app phanee47/capstone-app"
                      sh 'docker push phanee47/capstone-app'
                  }
              }
         }
         stage('Deploying') {
              steps{
                  echo 'Deploying to AWS...'
                  sh "pwd"   
                  sh "docker images"    
                  }
              }
        stage("Cleaning up") {
              steps{
                    echo 'Cleaning up...'
                    sh "docker system prune"
              }
        }
     }
}
