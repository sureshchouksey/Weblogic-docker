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
               //PORT = sh ( script : ("docker ps|grep weblogic${env.BRANCH_NAME}${currentBuild.number}|sed 's/.*0.0.0.0://g'|sed 's/->.*//g'"), returnStatus: true) 
               	//def PORT = sh (script: "(docker ps|grep some-container-name|sed 's/.*0.0.0.0://g'|sed 's/->.*//g')", returnStdout: true)
                //echo "${PORT}" 
                def gitChangeList = sh (script: "(git diff-tree --no-commit-id --name-only -r ${env.gitlabAfter})", returnStdout: true)
                String response = sh (                
                    script: "(git log -m -1 --name-status | grep -E '^[A-Z]\\b' | sort | uniq | sed -e 's/^\\w\\t*\\ *//')",
                    returnStdout: true
                ).trim();
                echo "Git response: - "+response;
                echo "${port}" 
            }
        }

       
    }
}
