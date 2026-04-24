pipeline {
    agent { label 'rhel9-agent-1' }

    stages {
        stage('Verify Agent') {
            steps {
                sh '''
                    hostname
                    whoami
                    pwd
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                    pkill -f "node index.js" || true

                    export PORT=5006
                    export JENKINS_NODE_COOKIE=dontKillMe

                    nohup npm start > nohup.out 2>&1 &

                    sleep 5
                    cat nohup.out
                '''
            }
        }

        stage('Verify Application') {
            steps {
                sh '''
                    curl -I http://localhost:5006
                '''
            }
        }
    }
}
