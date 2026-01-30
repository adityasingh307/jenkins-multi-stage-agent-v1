pipeline {
    agent none

    stages {

        stage('Build Backend') {
            agent {
                docker {
                    image 'node:18'
                    args '-p 3000:3000'
                }
            }
            steps {
                dir('backend') {
                    sh '''
                      npm install
                      node app.js &
                      sleep 3
                      curl http://localhost:3000
                    '''
                }
            }
        }

        stage('Build Frontend') {
            agent {
                docker {
                    image 'nginx:alpine'
                }
            }
            steps {
                dir('frontend') {
                    sh '''
                      mkdir -p /usr/share/nginx/html
                      cp index.html app.js /usr/share/nginx/html
                      nginx -g "daemon off;" &
                      sleep 2
                    '''
                }
            }
        }
    }
}
