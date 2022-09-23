pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                sh"
                yum install git clone
                git clone git@github.com:brajamatha123/automation-application.git
                "
            }
        }
        stage('ci') {
            steps {
                sh"
                zip -r html-jenkins-$BUILD_NUMBER.zip *
                aws s3 cp html-jenkins-$BUILD_NUMBER.zip s3://artifactory-cicd-html/
                "
            }
        }

        stage('deployment') {
            steps {
                sh"
                rm -fr *
                aws s3 cp s3://artifactory-cicd-html/html-jenkins-$PKG.zip .
                unzip html-jenkins-$PKG.zip
                scp index.html root@172.31.15.6:/var/www/html/
                "
            }
            
    
        }
        stage('validation') {
            
            steps {
                sh"
                curl -I http://13.38.103.238
                "



                
            }
        }
        
    }
}
