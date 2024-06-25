pipeline {
    agent any
    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-17'
        PYTHON_HOME = 'C:\\Python30'
        MAVEN_HOME = 'C:\\Maven\\bin'
        PATH = "${env.PATH};${JAVA_HOME}\\bin;${PYTHON_HOME};${MAVEN_HOME}"
    }
    stages {
        stage('Checkout') {
            steps {
                // Cloner le repository depuis GitHub
                git branch: 'master', url: 'https://github.com/mertilm/calculator.git'
            }
        }

        stage('Build') {
            steps {
                // Nettoyer et compiler le projet avec Maven
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests unitaires
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Packager le projet en JAR
                bat 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archiver les artefacts générés (JAR)
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Publier les résultats des tests, si disponibles
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
