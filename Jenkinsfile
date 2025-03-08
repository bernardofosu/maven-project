
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

// Multi stage Parallel pipeline exexuting maven build and archiving the war file
pipeline {
    agent {
        label 'agent-2'  // Default agent for all stages unless overridden
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
        stage("testing") {
            parallel {
                stage("Test A") {
                    agent {
                        label 'agent-1'  // Runs Test A on agent-1
                    }
                    steps {
                        echo "Running Test A"
                        sh "echo 'Executing Test A commands...'"
                    }
                }
                stage("Test B") {
                    agent {
                        label 'agent-2'  // Runs Test B on agent-2
                    }
                    steps {
                        echo "Running Test B"
                        sh "echo 'Executing Test B commands...'"
                    }
                }
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: '**/target/*.war'
        }
    }
}
