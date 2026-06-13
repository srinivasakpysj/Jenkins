pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }

    environment {
        COURSE = "Jenkins"
    }

    options {
        timeout(time: 10, unit: 'SECONDS')
        disableConcurrentBuilds()
    }

    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

    // This is build section information for reference
    stages {
        stage('Build') {
            steps {
                script {
                    sh """
                        echo "Building"
                        echo \$COURSE
                        env

                        echo "Hello ${params.PERSON}"
                        echo "Biography: ${params.BIOGRAPHY}"
                        echo "Toggle: ${params.TOGGLE}"
                        echo "Choice: ${params.CHOICE}"
                        echo "Password: ${params.PASSWORD}"
                    """
                }
            }
        }

        // This is Test section information for reference
        stage('Test') {
            steps {
                echo "Testing"
            }
        }

        // This is deploy section information for reference
        stage('Deploy') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"

                parameters {
                    string(
                        name: 'PERSON',
                        defaultValue: 'Mr Jenkins',
                        description: 'Who should I say hello to?'
                    )
                }
            }

            steps {
                echo "Deploying"
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello again!'
            cleanWs()
        }

        success {
            echo 'I will run if success'
        }

        failure {
            echo 'I will run if failure'
        }
    }
}

