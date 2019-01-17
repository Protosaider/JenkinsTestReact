// node {
//     env.AWS_ECR_LOGIN=true
//     def newApp
//     def registry = 'gustavoapolinario/microservices-node-todo-frontend'
//     def registryCredential = 'dockerhub'
	
// 	stage('Git') {
// 		git 'https://github.com/gustavoapolinario/node-todo-frontend'
// 	}
// 	stage('Build') {
// 		sh 'npm install'
// 	}
// 	stage('Test') {
// 		sh 'npm test'
// 	}
// 	stage('Building image') {
//         docker.withRegistry( 'https://' + registry, registryCredential ) {
// 		    def buildName = registry + ":$BUILD_NUMBER"
// 			newApp = docker.build buildName
// 			newApp.push()
//         }
// 	}
// 	stage('Registring image') {
//         docker.withRegistry( 'https://' + registry, registryCredential ) {
//     		newApp.push 'latest2'
//         }
// 	}
//     stage('Removing image') {
//         sh "docker rmi $registry:$BUILD_NUMBER"
//         sh "docker rmi $registry:latest"
//     }
    
// }

// pipeline {
//     agent {
//         docker {
//             image 'node:6-alpine'
//             args '-p 3000:3000'
//         }
//     }
//     environment {
//         CI = 'true'
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//         stage('Deliver') {
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//                 input message: 'Finished using the web site? (Click "Proceed" to continue)'
//                 sh './jenkins/scripts/kill.sh'
//             }
//         }
//     }
// }


		// node('ephemeral-slave') {
		//     // environment {
		//     //     CI = 'true' 
		//     // }
		//     withEnv(['CI=true']) { //CI - or use RUN CI=true npm test
		//     	try {

		//     		// stage('Start') {
		//     		// 	notifySlack()
		//     		// }

		// 			stage('Checkout') {
		// 				checkout scm
		// 			}

		// 			stage('Environment') {
		// 				sh 'git --version'
		// 				echo "Branch: ${env.BRANCH_NAME}"
		// 				sh 'docker -v'
		// 				sh 'printenv'
		// 			}

		// 			stage('Build Docker test') {
		// 				sh 'docker build --tag react-test --file Dockerfile.test --no-cache .'
		// 			}

		// 			stage('Docker test') {
		// 				sh 'docker run --rm react-test'
		// 			}

		// 			stage('Clean Docker test') {
		// 				sh 'docker rmi react-test'
		// 			}

		// 			stage('Deploy') {
		// 				if(env.BRANCH_NAME == 'master') {
		// 					sh 'docker build -t react-app --no-cache .'

		// 					sh 'docker tag react-app localhost:5000/react-app'
		// 					sh 'docker push localhost:5000/react-app'
		// 					sh 'docker rmi -f react-app localhost:5000/react-app'

		// 					// sh 'docker tag react-app http://192.168.99.100:5000/react-app'
		// 					// sh 'docker push http://192.168.99.100:5000/react-app'
		// 					// sh 'docker rmi -f react-app http://192.168.99.100:5000/react-app'
		// 				}
		// 			}
		// 	  	} catch (err) {
		// 	  		// currentBuild.result = 'FAILURE'
		// 	  		throw err
		// 	  	}
		// 		// } finally {
		// 		// 	notifySlack(currentBuild.result)
		// 		// }
		//     }
		// }
		// 


// def getGitUrl() {
//     def url = sh(returnStdout: true, script: "git remote get-url origin").trim()
//     return url
// }

// def getGitAuthor() {
//     def commit = sh(returnStdout: true, script: 'git rev-parse HEAD')
//     def author = sh(returnStdout: true, script: "git --no-pager show -s --format='%an' ${commit}").trim()
//     return author
// }

// def getLastCommitMessage() {
//     def message = sh(returnStdout: true, script: 'git log -1 --pretty=%B').trim()
//     return message
// }

import net.sf.json.JSONArray;
import net.sf.json.JSONObject;

// def notifySlack(String buildStatus = 'STARTED', String channel = '#build') {

//   long epoch = System.currentTimeMillis()/1000

//   // Build status of null means success.
//   buildStatus = buildStatus ?: 'SUCCESS'

//   def color

//   if (buildStatus == 'STARTED') {
//       color = '#D4DADF'
//       // color = 'good'
//   } else if (buildStatus == 'SUCCESS') {
//       color = '#BDFFC3'
//       // color = 'good'
//   } else if (buildStatus == 'UNSTABLE') {
//       color = '#FFFE89'
//       // color = 'warning'
//   } else if (status == 'ABORTED') {
//       color = '#FFFE89'
//       // color = 'warning'
//   } else if (status == 'NOT_BUILT') {
//       color = '#FFFE89'
//       // color = 'warning'
//   }
//   else if (buildResult == 'FAILURE') {
//       color = '#FFFE89'
//       // color = 'danger'
//   } 
//   else {
//       color = '#FF9FA1'
//   }

//   // get Jenkins user that has started the build
//   wrap([$class: 'BuildUser']) { script { env.USER_ID = "${BUILD_USER_ID}" } }

//   def subject = "${buildStatus}: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER} by ${env.USER_ID}"

//   def msg = "${subject}\n More info at: ${env.BUILD_URL}"

//   JSONArray attachments = new JSONArray();
//   JSONObject attachment = new JSONObject();

//   attachment.put('fallback', '${subject}');
//   attachment.put('pretext', 'Git info');
//   attachment.put('color', '$(color)');
//   def url = getGitUrl();
//   attachment.put('footer', '$(url)');

//   JSONObject fieldBranch = new JSONObject();
//   fieldBranch.put('title', 'Branch');
//   fieldBranch.put('value', '${env.BRANCH_NAME}');
//   fieldBranch.put('short', 'true');

//   JSONObject fieldGitAuthor = new JSONObject();
//   fieldGitAuthor.put('title', 'Author');
//   def author = getGitAuthor();
//   fieldGitAuthor.put('value', '${author}');
//   fieldGitAuthor.put('short', 'true');

//   JSONObject fieldLastCommitMessage = new JSONObject();
//   fieldLastCommitMessage.put('title', 'Last commit');
//   def lastCommitMessage = getLastCommitMessage();
//   fieldLastCommitMessage.put('value', '${lastCommitMessage}');
//   fieldLastCommitMessage.put('short', 'true');

//   JSONArray fields = new JSONObject();
//   fields.add(fieldBranch);
//   fields.add(fieldGitAuthor);
//   fields.add(fieldLastCommitMessage);

//   attachment.put('fields', fields);

//   attachments.add(attachment);

//   slackSend(color: color, message: msg, channel: channel, attachments: attachments.toString())
// }


// @Library('github.com/Protosaider/jenkins-shared-library@master') _ 
// @Library('jenkins-shared-library') _ 

pipeline {
	agent {
		node {
			label 'ephemeral-slave'
		}
	}

	options {
		skipDefaultCheckout()
	// 	disableConcurrentBuilds()
	// 	timeout(time: 10, unit: 'MINUTES')
	// 	buildDiscarder(logRotator(numToKeepStr: '10'))
	// 	timestamps()
	}

	parameters {

		string(name: 'SLACK_CHANNEL_1',
				description: 'Default Slack channel to send messages to',
				defaultValue: '#build')

		string(name: 'SLACK_CHANNEL_2',
				description: 'Default Slack channel to send messages to',
				defaultValue: '#my_channel_2')           
	}

	environment {
		// // Slack configuration
		// SLACK_COLOR_DANGER  = '#E01563'
		// SLACK_COLOR_INFO    = '#6ECADC'
		// SLACK_COLOR_WARNING = '#FFC300'
		// SLACK_COLOR_GOOD    = '#3EB991'
		CI = true
	}

	stages {

		stage('Checkout Git repository') {
			steps {
				checkout scm
				// wrap([$class: 'BuildUser']) { script { env.USER_ID = "${BUILD_USER_ID}" } }

				script {
					def url = sh(returnStdout: true, script: "git remote get-url origin").trim()
					def commit = sh(returnStdout: true, script: 'git rev-parse HEAD')
    				def author = sh(returnStdout: true, script: "git --no-pager show -s --format='%an' ${commit}").trim()
   	 				def lastCommitMessage = sh(returnStdout: true, script: 'git log -1 --pretty=%B').trim()
  					long epoch = System.currentTimeMillis()/1000
  					String buildStatus = 'STARTED'
  					def color = '#D4DADF'
  					// def subject = "${buildStatus}: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER} by ${env.USER_ID}"
  					def subject = "${buildStatus}: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}"
  					def msg = "${subject}\n More info at: ${env.BUILD_URL}"

					// JSONArray attachments = new JSONArray();
					// JSONObject attachment = new JSONObject();

					// attachment.put('fallback', '${subject}');
					// attachment.put('pretext', 'Git info');
					// attachment.put('color', '$(color)');

					// JSONObject fieldBranch = new JSONObject();
					// fieldBranch.put('title', 'Branch');
					// fieldBranch.put('value', '${env.BRANCH_NAME}');
					// fieldBranch.put('short', 'true');

					// JSONObject fieldGitAuthor = new JSONObject();
					// fieldGitAuthor.put('title', 'Author');
					// fieldGitAuthor.put('value', '${author}');
					// fieldGitAuthor.put('short', 'true');

					// JSONObject fieldLastCommitMessage = new JSONObject();
					// fieldLastCommitMessage.put('title', 'Last commit');
					// fieldLastCommitMessage.put('value', '${lastCommitMessage}');
					// fieldLastCommitMessage.put('short', 'true');

					// JSONArray fields = new JSONObject();
					// fields.add(fieldBranch);
					// fields.add(fieldGitAuthor);
					// fields.add(fieldLastCommitMessage);

					// attachment.put('fields', fields);

					// attachment.put('footer', '$(url)');
					// attachment.put('ts', '$(epoch)');

					// attachments.add(attachment);

					// def json = new groovy.json.JsonBuilder()
					// json {
					// 	attachments ([ 
					// 		{
					// 			fallback '${subject}'
					// 			color '$(color)'
					// 			pretext 'Git info'
					// 			fields([
					// 				{
					// 					title 'Branch'
					// 					value '${env.BRANCH_NAME}'
					// 					'short' true
					// 				}
					// 				{
					// 					title 'Author'
					// 					value '${author}'
					// 					'short' true
					// 				}
					// 				{
					// 					title 'Last commit'
					// 					value '${lastCommitMessage}'
					// 					'short' true
					// 				}
					// 			])
					// 			footer '$(url)'
					// 			ts '${epoch}'
					// 		}
					 
					// 	])
					// }
					// println json.toPrettyString()
					
					def json = """[ { \"fallback\": \"subject\" } ]"""

					// slackSend(color: color, message: msg, channel: channel, attachments: attachments.toString())
					// slackSend(color: color, message: msg, channel: channel, attachments: json.toPrettyString())
					slackSend(color: color, message: msg, channel: channel, attachments: json)
				}
			}
		}

		stage('Environment') {
			steps {
				sh 'git --version'
				echo "Branch: ${env.BRANCH_NAME}"
				sh 'docker -v'
				sh 'printenv|sort'
				sh 'env|sort'
			}
		}

		stage('Build Docker test') {
			steps {
				sh 'docker build --tag react-test --file Dockerfile.test --no-cache .'
			}
		}

		stage('Docker test') {
			steps {
				sh 'docker run --rm react-test'
			}
		}

		stage('Clean Docker test') {
			steps {
				sh 'docker rmi react-test'
			}
		}

		// stage('Deploy') {
		// 	when {
		// 		branch 'master'
		// 	}

		// 	steps {
		// 		sh 'docker build -t react-app --no-cache .'

		// 		sh 'docker tag react-app localhost:5000/react-app'
		// 		sh 'docker push localhost:5000/react-app'
		// 		sh 'docker rmi -f react-app localhost:5000/react-app'
		// 	}
		// }
		
		// stage("Clean Workspace") {
		// 	steps {
		// 		echo "Cleaning-up job workspace"
		// 		deleteDir()
		// 	}
		// }
	}

	post {
		always {
			echo "Sending message to Slack"
			// script {
			// 	notifySlack(buildStatus: currentBuild.result, channel: "${params.SLACK_CHANNEL_2}")
			// }
		}

		// aborted {
		// 	echo "Sending message to Slack"
		// 	// slackSend (color: "${env.SLACK_COLOR_WARNING}",
		// 	// 		channel: "${params.SLACK_CHANNEL_2}",
		// 	// 		message: "*ABORTED:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
		// }

		// failure {
		// 	echo "Sending message to Slack"
		// 	// slackSend (color: "${env.SLACK_COLOR_DANGER}",
		// 	// 		channel: "${params.SLACK_CHANNEL_2}",
		// 	// 		message: "*FAILED:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
		// }

		// success {
		// 	echo "Sending message to Slack"
		// 	// slackSend (color: "${env.SLACK_COLOR_GOOD}",
		// 	// 		channel: "${params.SLACK_CHANNEL_1}",
		// 	// 		message: "*SUCCESS:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${env.USER_ID}\n More info at: ${env.BUILD_URL}")
		// }

		// unstable {

		// }
	}
}
