pipeline {
    agent any  // Jenkins запустит сборку на любом доступном агенте

    stages {
        stage('Checkout') {
            steps {
                // Скачиваем код из GitHub
                git branch: 'master', url: 'https://github.com/Evgen-Domoslavskij/New_Repositori.git'
            }
        }

        stage('Install Newman') {
            steps {
                script {
                    // Устанавливаем Newman (если его нет)
                    bat 'npm install -g newman'
                }
            }
        }

        stage('Run Postman Tests') {
            steps {
                script {
                    // Запускаем коллекцию Postman через Newman
                    bat 'newman run my_collection.json -e my_environment.json --reporters cli'
                }
            }
        }

        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: '**/*.json', allowEmptyArchive: true
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
