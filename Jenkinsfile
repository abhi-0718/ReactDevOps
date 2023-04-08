pipeline {
     agent any
     stages {
        stage("Build") {
            steps {
                sh "npm install"
                sh "npm run build"
            }
        }

        stage('Creating Image of build') {
            steps{
                script {
                    echo '---------------------------Building Image----------------------------------'
                    sh 'docker build -t habhi/react_devops .'
                    //build will serach for dockerfile in repository
                    echo '---------------------------Image Successfully Build---------------------------------'
                }
            }
        }

        stage('Pushing image to DockerHub') {
            steps{
                script{
                    echo '-----------------------------Pushing Image----------------------------------------'
                    docker.withRegistry('', '83626bcd-d2fa-4b05-83e0-1a4436f8804d') {
                        sh 'docker push habhi/react_devops'
                        echo '-------------------------Image Successfully pushed--------------------------------'
                    }
                } 
            }
        }

        stage('Running container'){
            steps{
                script{
                    echo '-----------------------------Running Container-------------------------------------'
                    sh 'docker run --name react-app -d -p 80:80 habhi/react_devops ' 
                }
            }
        }
        stage("Deploy") {
            steps {
                sh "rm -rf /var/www/react-app"
                sh "cp -r ${WORKSPACE}/build/ /var/www/react-app/"
            }
        }
    }
}