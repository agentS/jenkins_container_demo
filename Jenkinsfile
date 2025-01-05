pipeline {
	agent {
		label "!windows"
	}

	stages {
		stage("build") {
			environment {
				RANDOM_NUMBER = "${Math.abs(new Random().nextInt(32768))}"
			}
			steps {
				echo "Let's go to the mall today!"
				sh '''
					echo "Multiline shell steps work too! :)"
					java -version
				'''

				retry(1) {
					sh '''
						if [ ${RANDOM_NUMBER} -lt 16535 ]; then
							echo "Sideshow Bob"
							exit 1
						else
							echo "Kippers for breakfast, Aunt Helga?"
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
			deleteDir()
		}
		success {
			echo "This command will only run in case of a successful build"
			mail to: "lukas.schoerghuber@posteo.at",
				 subject: "Succeeded Pipeline: ${currentBuild.fullDisplayName}",
				 body: "Build results available at ${env.BUILD_URL}"
		}
		failure {
			echo "This will run only in case of a failed build"
			mail to: "lukas.schoerghuber@posteo.at",
				 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
				 body: "Something is wrong with ${env.BUILD_URL}"
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
