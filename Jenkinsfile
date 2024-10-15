pipeline{
    agent{
        node{
            label 'agent-ec2-01'
        }
    }
    options{
        buildDiscarder logRotator(
            daysToKeepStr: '15',
            numToKeepStr: '10'
        )
    }
    stages{
        stage('Clean Workspace'){
            steps{
                cleanWs()
                echo "*** Successfully cleaned the Workspace ***"
            }
        }
        stage('Checkout'){
            checkout([
                $class: 'GitSCM',
                branches: [[name: "*/main"]],
                userRemoteConfigs: [[url:"https://github.com/eswarmaganti/jenkins-multi-branch-pipeline.git"]]
            ])
        }
        stage('Code Analysis'){
            steps{
                echo "*** Successfully completed sonarqube code analysis ***"
            }
        }
        stage('Unit Testing'){
            steps{
                echo "*** Successfuly completed unit testing ***"
            }
        }
        stage('Deploy to STAGE & PRE_PROD Environments'){
            when{
                branch 'dev'
            }
            steps{
                echo '*** Successfully Deployed the application to STAGE Enviroment'
                echo '*** Successfully Deployed the application to PRE-PROD Enviroment'
            }
        }
        stage('Deploy to PROD Environments'){
            when{
                branch 'main'
            }
            steps{
                echo '*** Successfully Deployed the application to PROD Enviroment'
            }
        }   
    }
}