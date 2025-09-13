pipeline {
    agent any // Or specify a specific agent, e.g., agent { docker 'maven:3.8.1-jdk-11' }

    tools {
        // Ensure Maven is configured in Jenkins Global Tool Configuration
        maven 'Maven' 
        // Ensure JDK is configured in Jenkins Global Tool Configuration
        jdk 'JDK_17' 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/your-spring-boot-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests' // Build without running tests initially
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test' // Run unit and integration tests
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package' // Create the executable JAR/WAR file
            }
        }

        // Optional: Add a deployment stage
        stage('Deploy') {
            steps {
                echo 'Deployment skipping!'
                // Example: Copy the JAR to a remote server or deploy to a container orchestrator
                // sh 'scp target/*.jar user@remote-server:/path/to/deploy'
                // Or, if using Docker:
                // script {
                //     docker.build("your-spring-boot-app:${env.BUILD_NUMBER}")
                //     docker.withRegistry('https://your-docker-registry', 'your-docker-credentials') {
                //         docker.image("your-spring-boot-app:${env.BUILD_NUMBER}").push()
                //     }
                // }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
            // Add notifications or post-success actions here
        }
        failure {
            echo 'Pipeline failed!'
            // Add notifications or post-failure actions here
        }
    }
}
