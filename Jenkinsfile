pipeline {
    agent any

    stages {
        
        stage ('Build Docker') {

            steps {
                sh 'docker pull ashishfulcrum/weblogic_server:11g'
            }
        }

        stage ('Run Docker') {
            
            steps {
                echo "${env.BRANCH_NAME}"
                echo "${currentBuild.number}"
                //bat ("docker stop spring${env.BRANCH_NAME}${currentBuild.number}")
                //bat ("docker rm spring${env.BRANCH_NAME}${currentBuild.number}")
                sh ("docker run --name weblogic${env.BRANCH_NAME}${currentBuild.number} -d -p 7001 ashishfulcrum/weblogic_server:11g")
               sh ("docker ps|grep weblogic${env.BRANCH_NAME}${currentBuild.number}|sed 's/.*0.0.0.0://g'|sed 's/->.*//g'")
               	//def PORT = sh (script: "(docker ps|grep some-container-name|sed 's/.*0.0.0.0://g'|sed 's/->.*//g')", returnStdout: true)
                //echo "${PORT}" 
            }
        }

       
    }
}
