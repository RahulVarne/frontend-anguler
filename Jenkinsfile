pipeline {
    agent any
    stages {
        stage('pull'){
            steps {
                git branch: 'main', url: 'https://github.com/RahulVarne/frontend-anguler.git'
            }
        }
        stage('build'){
            steps {
                sh '''
                    npm install
                    ng build
                '''
            }
        }
        stage('deploy'){
            steps {
                withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                sh ''' 
                    aws s3 cp --recursive dist/angular-frontend/ s3://cbz-bucket-1-1/
                ''' 
                }               
            }

        }
    }
}