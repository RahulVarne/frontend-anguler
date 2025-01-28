pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/RahulVarne/frontend-anguler.git'
            }
        }
        stage('Install Dependencies & Build') {
            steps {
                sh '''
                    npm install
                    ng build --configuration production
                '''
            }
        }
        stage('Deploy to S3') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        aws s3 sync dist/angular-frontend/ s3://cbz-bucket-1-1/ --delete
                    '''
                }
            }
        }
    }
}
