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

node('ephemeral-slave') {
    environment {
        CI = 'true' 
    }
	try {
		stage('Checkout') {
			checkout scm
		}

		stage('Environment') {
			sh 'git --version'
			echo "Branch: ${env.BRANCH_NAME}"
			sh 'docker -v'
			sh 'printenv'
		}

		stage('Build Docker test') {
			sh 'docker build --tag react-test --file Dockerfile.test --no-cache .'
		}

		stage('Docker test') {
			sh 'docker run --rm react-test'
		}

		stage('Clean Docker test') {
			sh 'docker rmi react-test'
		}

		stage('Deploy') {
			if(env.BRANCH_NAME == 'master') {
				sh 'docker build -t react-app --no-cache .'

				sh 'docker tag react-app localhost:5000/react-app'
				sh 'docker push localhost:5000/react-app'
				sh 'docker rmi -f react-app localhost:5000/react-app'

				// sh 'docker tag react-app http://192.168.99.100:5000/react-app'
				// sh 'docker push http://192.168.99.100:5000/react-app'
				// sh 'docker rmi -f react-app http://192.168.99.100:5000/react-app'
			}
		}
  	} catch (err) {
  		throw err
	}
}
