pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        nodejs "nodejs"
    }

    stages {
    stage('Checkout') {
            steps {
                // Install Node.js and npm (if not already installed)
                // You can also use a specific Node.js version if you configured it in Jenkins.
                // Install the project dependencies using npm or yarn.
                git "https://github.com/sereyatiampati/gallery"
            }
        }
     stage('Install Dependencies') {
            steps {
                // Install Node.js and npm (if not already installed)
                // You can also use a specific Node.js version if you configured it in Jenkins.
                // Install the project dependencies using npm or yarn.
                sh 'npm install'
            }
        }
    stage('test'){
            post{
                failure{
                    mail bcc: '', body: 'The npm test failed. Build status failed.', cc: '', from: '', replyTo: '', subject: 'Failed test', to: 'sereyatiampatistudies@gmail.com'
                }
                success{
                mail bcc: '', body: 'The build and Test were successful. App deploying to Render. Expect a Slack notification once done.', cc: '', from: '', replyTo: '', subject: 'Build and Test success', to: 'sereyatiampatistudies@gmail.com'
                }
        
            }
            steps{
               sh 'npm test'
            }
        }
        

    stage('Deploy to Render') {
          steps {
             withCredentials([usernameColonPassword(credentialsId: 'render', variable: 'RENDER_CREDENTIALS' )]){
                   //   git push https://api.render.com/deploy/srv-ciqrl0tgkuvrtodr97ig?key=tMGf0zvYjew
              sh '''
          
              curl -X POST https://api.render.com/deploy/srv-ciqrl0tgkuvrtodr97ig?key=tMGf0zvYjew
              '''
            }
          }
        }
    stage('Slack notification'){
            steps{
                slackSend channel: '#emillyip1', color: '#008000', message: "Deployment of ${BUILD_ID} to render successful. Click the link to view results. https://gallery-nnku.onrender.com/", tokenCredentialId: 'emillyip1'
            }
        }
        
    }
 
}

