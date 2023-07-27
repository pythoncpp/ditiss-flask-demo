pipeline {
    agent any
    stages {
        stage ('SCM checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/pythoncpp/ditiss-flask-demo.git'
            }
        }
        stage ('docker image build') {
            steps {
                sh '/usr/bin/docker image build -t pythoncpp/flask-demo-image .'
            }
        }
        stage ('docker login') {
            steps {
                sh 'echo dckr_pat_WiG2NZJ8py7I1a1MaIPEdPjoJSI | /usr/bin/docker login -u pythoncpp --password-stdin'
            }
        }
        stage ('docker image push') {
            steps {
                sh '/usr/bin/docker image push pythoncpp/flask-demo-image'
            }
        }
        stage ('get the confirmation from user') {
            steps {
                input 'Do you want to deploy this application?'
            }
        }
        stage ('remove existing service') {
            steps {
                sh '/usr/bin/docker service rm flask-service'
            }
        }
        stage ('create docker service') {
            steps {
                sh '/usr/bin/docker service create --name flask-service -p 4000:4000 --replicas 2 pythoncpp/flask-demo-image'
            }
        }
    }
}
