pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git '/home/Downloads/GitHub/JenkinsDependencyCheckTest'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
			}
		}
    stage('Build') {
			steps {
				sh 'composer install'
			}
		}
		stage('Test') {
			steps {
                		sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
            		}
		}

	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
    always	{
			junit testResults: 'logs/unitreport.xml'
		}

	}
}
