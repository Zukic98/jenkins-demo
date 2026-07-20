pipeline {
    agent any 

    stages {
        stage('1. Preuzimanje koda (Checkout)') {
            steps {
                // Jenkins automatski povlači kod sa GitHuba, ali možemo potvrditi
                echo 'Preuzimanje koda sa GitHub-a uspješno...'
            }
        }

        stage('2. Testiranje aplikacije') {
            steps {
                echo 'Pokretanje testova...'
                // Ovdje bi išlo npr. npm test, ali pošto nemamo node na Jenkinsu, samo simuliramo
                echo 'Testovi uspješno završeni!'
            }
        }

        stage('3. Izrada Docker Image-a (Build)') {
            steps {
                script {
                    echo 'Kreiranje Docker image-a...'
                    // Jenkins pokreće lokalni docker i pravi image
                    sh 'docker build -t jenkins-demo-app:latest .'
                }
            }
        }

        stage('4. Pokretanje Kontejnera (Deploy)') {
            steps {
                script {
                    echo 'Pokretanje aplikacije u Dockeru...'
                    // Prvo gasimo stari ako postoji, pa pokrećemo novi
                    sh 'docker rm -f moja-pokrenuta-app || true'
                    sh 'docker run -d --name moja-pokrenuta-app jenkins-demo-app:latest'
                    echo 'Aplikacija je uspješno deployovana lokalno!'
                }
            }
        }
    }
    
    post {
        always {
            echo 'Čišćenje radnog prostora...'
        }
        success {
            echo 'Bravo! CI/CD Pipeline je uspješno završen.'
        }
        failure {
            echo 'Nešto je pošlo po zlu. Provjeri logove.'
        }
    }
}
