pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Clean') {
            steps {
                sh 'rm -rf out'
            }
        }
        stage('Transform') {
            agent {
                docker {
                    image 'cloudfluff/databaker'
                    reuseNode true
                }
            }
            steps {
                sh "jupyter-nbconvert --to python --stdout GEONOM-to-RDF.ipynb | python"
            }
        }
    }
    post {
        always {
            archiveArtifacts 'out/*'
        }
    }
}
