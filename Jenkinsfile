pipeline{
    agent {
        label 'agent-2'
    }
    tools {
        maven 'mymaven'
    parameters {
        string defaultValue: 'ofosu', name: 'LASTNAME'
    }
    environment {
        NAME = "kwasi"
        }

    }
    stages {
        stage("build") {
            steps {
                  sh "mvn clean package"
                  echo "Hello $NAME ${params.LASTNAME}"
            }
            post {
                success {
                  archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}