pipeline {
    agent none
    stages {
        stage("Build") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                script {
                    for (int i=0; i<10; i++) {
                        echo("Script ${i}")
                    }
                }
                echo("Start Build")
                sh("chmod +x ./mvnw")
                sh("./mvnw clean compile test-compile")
                echo("Finish Build")
            }
        }
        stage("Test") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                script {
                    def data = [
                        "firstName":"Angga",
                        "lastName":"Wijaya"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo("Start Test")
                sh("chmod +x ./mvnw")
                sh("./mvnw test")
                echo("Finish Test")
            }
        }
        stage("Deploy") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Hello Deploy 1")
                sleep(5)
                echo("Hello Deploy 2")
                echo("Hello Deploy 3")
            }
        }
    }
    post {
        always {
            echo "I will always say Hello again!"
        }
        success {
            echo "Yay, success"
        }
        failure {
            echo "Oh no, a failure"
        }
        cleanup {
            echo "Don't care success or error"
        }
    }
}