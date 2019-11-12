import java.text.SimpleDateFormat
import groovy.transform.Field
import java.util.regex.Matcher
import java.util.regex.Pattern
import java.nio.file.*;

def  browser = 'Unknown'

pipeline {
     environment {
            port = "32772"
        }
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
                //sh ("docker run --name weblogic${env.BRANCH_NAME}${currentBuild.number} -d -p 7001 ashishfulcrum/weblogic_server:11g")
               //sh ("docker ps|grep weblogic${env.BRANCH_NAME}${currentBuild.number}|sed 's/.*0.0.0.0://g'|sed 's/->.*//g'") 
               sh ("docker ps|grep weblogicmaster1|sed 's/.*0.0.0.0://g'|sed 's/->.*//g'") 
               //port = sh (script: "docker ps|grep weblogicmaster1|sed 's/.*0.0.0.0://g'|sed 's/->.*//g'", returnStdout: true).trim()
               	// port = "32773";
                //  echo 'Building Environment: ' + port
            }
        }

         stage('Example') {
            steps {
                script {
                    browser = sh(returnStdout: true, script: "docker ps|grep weblogicmaster1|sed 's/.*0.0.0.0://g'|sed 's/->.*//g'")
                }
            }
        }

       
    }
}
