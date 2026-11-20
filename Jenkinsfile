
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Starting Build Stage'
                sh '''
                    python3 -m venv .venv
                    .venv/bin/pip install -r requirements.txt
                '''
                echo 'Build completed successfully'
            }
        }

        stage('Test') {
            steps {
                echo 'Starting Test Stage'
                sh '''
                    .venv/bin/python -m unittest discover -s . -p "test_*.py" -v
                '''
                echo 'All tests passed'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Starting Deploy Stage'
                sh '''
                    mkdir -p deployment
                    cp app.py deployment/
                    cp requirements.txt deployment/
                    echo "Deployment successful" > deployment/DEPLOYMENT.txt
                    ls -l deployment/
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the stage logs.'
        }
    }
}
