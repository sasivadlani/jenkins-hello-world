pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        jdk "jdk"
        maven "M398"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                // git branch: 'main', url: 'https://github.com/sasivadlani/jenkins-hello-world.git'
                // Run Maven on a Unix agent.
                sh "mvn clean package -DskipTests=true"
                archiveArtifacts artifacts: 'target/hello-demo-*.jar', followSymlinks: false
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Test') {
            steps {
                sh "mvn test"
                junit keepTestNames: true, stdioRetention: '', testResults: 'target/surefire-reports/TEST-*.xml'
            }
        }
    }
}
