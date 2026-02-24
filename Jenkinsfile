pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                    # 문제 발생 시 도움이될 정보들 출력
                    ls -la
                    node --version
                    npm --version
                    # -------------------------------
                    npm ci
                    npm run build
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
    }
}
