pipeline {
    agent any

    // 모든 stage가 동일한 Docker 컨테이너에서 실행됨
    // agent {
    //     docker {
    //         image 'node:18-alpine'
    //         reuseNode true
    //     }
    // }

    stages {
        stage('Build') {
            // stage마다 따로 agent를 두는 경우
            // 각 stage마다 별도의 실행 환경
            // 컨테이너도 각각 새로 뜸
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
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
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
