pipeline {
    agent any

    stages {
        stage('Validate') {
            steps {
                echo 'Building..'
		sh '/usr/share/maven/bin/mvn validate'
            }
        }
        stage('Build') {
            steps {
                echo 'Testing..'
		sh '/usr/share/maven/bin/mvn package'
            }
        }
        stage('Test') {
            steps {
		    deploy adapters: [tomcat9(credentialsId: 'github', path: '', url: 'http://54.236.49.125:8080/')], contextPath: null, war: '**/*.war'
                echo 'Deploying....'
		sh '/usr/share/maven/bin/mvn test'
            }
        }
    }
}
