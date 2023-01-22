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
		    sshagent(['tomcat']) {
    scp -o /var/lib/jenkins/workspace/Web-calculator/target/webapp-0.2.war 
}
		deploy adapters: [tomcat9(credentialsId: 'github-git', path: '', url: 'http://100.26.11.88:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
