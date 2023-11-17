pipeline{
    agent any
    tools {
        maven 'jdk17'
    }

    stages{
        stage ('Build'){
            steps{
                bat 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Tomcat Server') {
            steps{
                deploy adapters: [tomcat9(path: '', url: 'http://localhost:8090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
