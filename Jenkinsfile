pipeline {
	agent {
		label "!windows"
	}

	environment {
		RANDOM_NUMBER = "${Math.abs(new Random().nextInt(32768))}"
	}

	stages {
		stage("build") {
			steps {
				echo "Let's go to the mall today!"
				sh '''
					echo "Multiline shell steps work too! :)"
					java -version
				'''

				retry(3) {
					sh '''
						if [ ${Math.abs(new Random().nextInt(32768))} -lt 16535 ]; then
							echo "Sideshow Bob"
							$? = 1
						else
							echo "Kippers for breakfast, Aunt Helga?"
							$? = 0
						fi
					'''
				}

				timeout(time: 3, unit: "SECONDS") {
					echo "just for reference purposes"
				}
			}
		}
	}
	post {
		always {
			echo "And I will always love you!"
		}
		success {
			echo "This command will only run in case of a successful build"
		}
		failure {
			echo "This will run only in case of a failed build"
		}
		unstable {
			echo "This will run only if the run was marked as unstable"
		}
		changed {
			echo "This will run only if the state of the Pipeline has changed"
			echo "For example, if the Pipeline was previously failing but is now successful"
		}
	}
}
