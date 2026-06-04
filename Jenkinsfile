pipeline {
    agent {
        docker {
            image 'chialab/php-devops:8.2'
            args '-u root'
        }
    }
    stages {
        stage('Clone Repository') {
            steps {
                echo 'Récupération du code source...'
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                echo 'Installation de Composer et des paquets...'
                sh 'composer install -q --no-ansi --no-interaction --no-scripts --no-progress --prefer-dist'
            }
        }
        stage('Laravel Check') {
            steps {
                echo 'Configuration de l environnement Laravel...'
                sh 'cp -n .env.example .env || true'
                sh 'php artisan key:generate'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Exécution des tests automatisés...'
                sh 'php artisan test'
            }
        }
    }
}