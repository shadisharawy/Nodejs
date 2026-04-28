pipeline {
    agent { label 'rhel9-agent-1' }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Show Environment') {
            steps {
                sh 'hostname'
                sh 'whoami'
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Stop Old App If Running') {
            steps {
                sh '''
                    pkill -f "node index.js" || true
                    pkill node || true
                '''
            }
        }

        stage('Deploy App') {
            steps {
                sh '''
		    export PORT=5006
		    export JENKINS_NODE_COOKIE=dontKillMe
                    nohup npm start > app.log 2>&1 &
                    sleep 5
                '''
            }
        }

        stage('Verify App') {
            steps {
                sh 'curl -I http://localhost:5006 || true'
            }
        }
    }
}
