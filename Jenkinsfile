pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('Cloning repo') {
            steps {
                git credentialsId: 'git_credentials', url: 'https://github.com/shashikanth-t/mwebrepo.git'
                echo 'Code Checkout done sucessfully.'
            }
			}
            stage('Code build ') {
            steps {
            sh 'mvn clean package'
            echo 'Code build done sucessfully.'
            }
            }
            stage('Code deploy') {
            steps {
            sshagent(['deploy_user']) {
			sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@18.218.83.148:/opt/apache-tomcat-9.0.75/webapps"
				}
            }
            }            

        }
    }
