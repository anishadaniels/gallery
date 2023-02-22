pipeline{
    agent any
    tools{nodejs 'node'}
    stages{
        stage('software installations and git cloning'){
        steps{ git 'https://github.com/anishadaniels/gallery.git'
        sh 'npm install'
       
        }
        }
       
    
        stage('Build'){
            steps{
                echo'build succesful'
            }
        }
        stage('Tests'){
            steps {
                sh 'npm test'}
        }
        stage('deploy to render'){
            steps{
                httpRequest httpMode: 'POST', responseHandle: 'NONE', url: 'https://api.render.com/deploy/srv-cfpodbarrk0fd9vgapqg?key=mK7t1pfKCkQ', wrapAsMultipart: false
                echo 'Deploy to render was a success'
               
            }
        }


    }
    post {
    success {
       slackSend channel: 'daniels_ip1', message: "For build  ${env.JOB_NAME} build ${env.BUILD_ID}  the site is live at https://gallery-gt7q.onrender.com"
    }
    failure {
        mail body: 'Failed Build #'+BUILD_NUMBER+'',  subject: 'Error Build #'+BUILD_NUMBER+'', to: 'anisha.daniels@student.moringaschool.com'
    }
  }
}
