pipeline {
    agent none
    environment {
        AUTHOR = "Angga Wijaya"
        EMAIL = "anggawijaya7122@gmail.com"
        WEB = "https://aboutmeanggawijaya.blogspot.com"
        APP = credentials("angga_rahasia")
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }
    parameters {
        string(name:'NAME', defaultValue:'Guest',description:'What is your name?')
        text(name:'DESCRIPTION',defaultValue:'',description:'Tell me about you')
        booleanParam(name:'DEPLOY',defaultValue:false,description:'Need to deploy?')
        choice(name:'SOCIAL MEDIA',choices:['Instagram', 'Facebook', 'Twitter'],description:'Which social media?')
        password(name:'SECRET',defaultValue:'',description:'Encrypt Key')
    }
    stages {
        stage("Parameter") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Hello ${params.NAME}")
                echo("Description: ${params.DESCRIPTION}")
                echo("Deploy: ${params.DEPLOY}")
                echo("Social Media: ${params.SOCIAL_MEDIA}")
                echo("Secret: ${params.SECRET}")
            }
        }
        stage("Prepare") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("App User : ${APP_USR}")
                echo("App Password : ${APP_PSW}")
                sh('echo "App Password with kutip satu : $APP_PSW" > "rahasia.txt"')
                echo("Author : ${AUTHOR}")
                echo("Email Author : ${EMAIL}")
                echo("Website Author : ${WEB}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }
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