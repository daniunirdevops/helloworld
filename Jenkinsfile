pipeline {
    // utilitzem agent windows
    agent { label 'linux'}
    
    stages {
        stage ('inici') {
            steps {
                sh '''
                whoami
                '''
            }
        }
        // obtenim el codi del repostori remot
        stage('Checkout') {
            steps {
                checkout scm
                sh '''
                ls -al
                '''
            }
        }

        // executem els tests unitaris
        stage('Test') {
            steps {
                sh '''
                    export PYTHONPATH="$WORKSPACE"
                    python -m pytest test/unit --junitxml=result-unit.xml 
                '''
            }
        }
        
        // construim els resultats
        stage ('Results') {
            steps {
                junit 'result*.xml'
            }
        }
        
        
    }
}
