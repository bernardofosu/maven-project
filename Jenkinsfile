pipeline {
    agent any  // No default agent; each stage defines its own agent if use none here
    parameters {
        string defaultValue: 'ofosu', name: 'LASTNAME'
    }
    environment {
        NAME = "kwasi"
    }
    stages {
        stage("Testing") {
            parallel {
                stage("Test A") {
                    agent {
                        label 'agent-1'  // Runs on agent-1
                    }
                    steps {
                        echo "Running Test A"
                        sh "echo 'Executing Test A commands...'"
                    }
                }
                stage("Test B") {
                    agent {
                        label 'agent-2'  // Runs on agent-2
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
