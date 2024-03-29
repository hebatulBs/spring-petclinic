pipeline{
    agent any
    
    stages{
        
        stage("checkout"){
            steps{
                sh "ls"
                git branch: 'main', url:'https://github.com/hebatulBs/spring-petclinic'
                sh "ls"
            }
        }
        
        stage("build"){
           steps{
                sh "./mvnw package"
           }
        }
        
        stage("capture"){
            steps{
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml'
            }
        }
        
    }
    
    post{
        always{
            emailext body: '${env.BUILD_URL}\\n${current.Build.absoluteUrl}', 
             recipientProviders: [developers()], 
             subject: '${currentBuild.currentResult}: Job {env.JOB_NAME} (${env.BUILD_NUMBER})', 
             to: 'demo@test.com'
        }
    }

}
