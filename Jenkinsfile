pipeline {
    agent any

    stages {
        stage('Validate') {
            steps {
                echo 'Building..'
		sh '/usr/share/maven/bin/mvn clean validate'
            }
        }
	    
        stage('Build') {
            steps {
                echo 'Building..'
		sh '/usr/share/maven/bin/mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		sh '/usr/share/maven/bin/mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
		    sshagent(['Deploy-user']) {
    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Web-calculator/target/webapp-0.2.war ubuntu@44.204.197.108:/opt/tomcat/webapps"
		}

            }
        }
    }
}




