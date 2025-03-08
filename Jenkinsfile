
/*
// Single stage pipeline exexuting maven build and archiving the war file
pipeline {
    agent {
        label 'agent-2'
    }
    tools {
        maven 'mymaven'
    }
    parameters {
        string defaultValue: 'ofosu', name: 'LASTNAME'
    }
    environment {
        NAME = "kwasi"
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
*/

// Parallel stages pipeline
pipeline {
    agent {
        label 'agent-2'
    }
    tools {
        maven 'mymaven'
    }
    parameters {
        string defaultValue: 'ofosu', name: 'LASTNAME'
    }
    environment {
        NAME = "kwasi"
   }
    stages {
        stage("build") {
            steps {
                  sh "mvn clean package"
                  echo "Hello $NAME ${params.LASTNAME}"
            }
        }
        stage("deploy") {
            parallel {
                stage("deploy-to-dev") {
                    agent {
                        label 'agent-1'
                    }
                    steps {
                        echo "Deploying to dev"
                    }
                }
                stage("deploy-to-prod") {
                    agent {
                        label 'agent-2'
                    }
                    steps {
                        echo "Deploying to prod"
                    }
                }
            }
            post {
                success {
                  archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}