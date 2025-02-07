pipeline {
    agent any
    environment {

        EMAIL_BODY = 

        """

            <p>EXECUTED: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER})\'</b></p>

            <p>

            View console output at 

            "<a href="${env.BUILD_URL}">${env.JOB_NAME}:${env.BUILD_NUMBER}</a>"

            </p> 

            <p><i>(Build log is attached.)</i></p>

        """

        EMAIL_SUBJECT_SUCCESS = "Status: 'SUCCESS' -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'" 

        EMAIL_SUBJECT_FAILURE = "Status: 'FAILURE' -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'" 

        EMAIL_RECEPIENT = 'sereyatiampatistudies@gmail.com'

    }


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
                    mail bcc: '', body: EMAIL_SUBJECT_FAILURE, cc: '', from: '', replyTo: '', subject: 'Failed test', to: EMAIL_RECEPIENT
                }
                success{
                mail bcc: '', body: EMAIL_SUBJECT_SUCCESS, cc: '', from: '', replyTo: '', subject: 'Build and Test success', to: EMAIL_RECEPIENT
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
    // post {
    //     success {
    //         emailext attachLog: true, 
    //             body: EMAIL_BODY, 

    //             subject: EMAIL_SUBJECT_SUCCESS,

    //             to: EMAIL_RECEPIENT
    //     }

    //     failure {
    //         emailext attachLog: true, 
    //             body: EMAIL_BODY, 

    //             subject: EMAIL_SUBJECT_FAILURE, 

    //             to: EMAIL_RECEPIENT
    //     }
    // }

 
}

