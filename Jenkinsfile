pipeline{
    agent any

    environment {
        OPENAI_API_KEY = credentials ( 'OPENAI_apikey')
        PORT = '3000'
    }

    stages {
        stage ('checkout')
        steps{
            branch: 'main',
            url : 'https://github.com/VarunC-S/chatgpt_clone_project.git'
        }
        stage ('build a docker image')
        steps{
            sh ' docker build -t chatgpt_clone .'
        }
        stage ('deploying the app')
        steps{
            script {
                sh """
                docker stop chatgpt_clone_container | true
                docker rm chatgpt_clone_container | true
                docker run -d \
                --name chatgpt_clone_container \
                -p 3000 \
                -e OPENAI_API_KEY = '${OPENAI_API_KEY}'
                -e PORT = '${PORT}' \
                chatgpt_clone
                """
            }
        }
    }

}