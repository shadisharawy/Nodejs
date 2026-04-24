pipeline {
    agent {label 'nodejs'}

    stages {
        stage('Clone Code') {
            steps {
                echo 'Cloning repository...'
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
                    export JENKINS_NODE_COOKIE=dontKillMe
                    nohup npm start > nohup.out 2>&1 &
                    sleep 5
                    cat nohup.out
                '''
            }
        }
	stage('Check Agent') {
	  steps {
  		 sh 'hostname'
            } 
}
    }
}
