pipeline {
	environment {
		project = "https://github.com/pannoi/juice-shop.git"
		containerName = "magazinSokov"
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
						echo 'units'
					}
				}
				stage ('run lint') {
					steps {
						echo 'lints'
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