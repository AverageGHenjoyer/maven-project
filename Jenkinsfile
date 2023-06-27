pipeline{
    agent any
    stages{
        stage('Build application'){
            steps{
                sh 'mvn -f my-app/pom.xml clean package'
            }
            post{
                success{
                    echo "Now archiving the Artifacts..."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Deploy in Staging Environment'){
            steps{
                build job: 'Deploy_Application_Staging_Env'
            }
        }
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'MINUTES'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                build job: "Deploy_Application_Prod_Env"
            }
            
        }
    }
}