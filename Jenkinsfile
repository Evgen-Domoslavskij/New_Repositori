pipeline {
    agent any  // Jenkins запустит сборку на любом доступном агенте

    stages {
        stage('Checkout') {
            steps {
                // Скачиваем код из GitHub
                git branch: 'main', url: 'https://github.com/Evgen-Domoslavskij/New_Repositori.git'
            }
        }

        stage('Install Newman') {
            steps {
                script {
                    // Устанавливаем Newman (если его нет)
                    sh 'npm install -g newman'
                }
            }
        }

        stage('Run Postman Tests') {
            steps {
                script {
                    // Запускаем коллекцию Postman через Newman
                    sh 'newman run my_collection.json -e my_environment.json --reporters cli'
                }
            }
        }

        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: '**/newman/*.json', fingerprint: true
            }
        }
    }

    post {
        always {
            echo "Pipeline завершён"
        }
        success {
            echo "Тесты успешно прошли!"
        }
        failure {
            echo "Ошибка в тестах! Проверьте лог."
        }
    }
}