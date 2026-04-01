pipeline{
    agent any
    tools{
        maven "Maven"
    }

    stages{
        stage ('Build'){
            steps{
                sh "mvn clean package"
            }
            post{
                success{
                    echo"Archiving the artifacts"
                    archiveArtifacts artifacts:'**/target/*.war'
                }
            }
        }
        stage('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat-server', path: '', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'
                
            }
        }

    }
}