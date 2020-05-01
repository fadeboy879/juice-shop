pipeline {
	environment {
		project = "https://github.com/fadeboy879/juice-shop.git"
		containerName = "magazin-sokov"
	}
	agent any
	options {
		timeout(time: 1, unit: 'HOURS')
	}
	stages {
		stage ('preparation') {
			steps {
				deleteDir()
			}
		}
		stage ('get src') {
			steps {
				git url: "${project}"
			}
		}
		stage ('get dependency') {
			steps {
				echo 'npm install'
			}
		}
		stage ('run tests') {
			parallel {
				stage ('run unit') {
					steps {
						echo 'npm run test'
					}
				}
				stage ('run lint') {
					steps {
						echo 'npm lint'
					}
				}
			}
		}
		stage ('build') {
			steps {
				script {
					dockerImage = docker.build("${containerName}", ".")
				}
			}
		}
	}
}