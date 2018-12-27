pipeline {

	// agent none
	agent { 'testslave' }

    environment {
        PATH_TO_PROJECT_ROOT = 'app/'
        // PATH_TO_MSBUILD = 'C:/"Program Files (x86)"/"Microsoft Visual Studio"/2017/Community/MSBuild/15.0/Bin/'
        // PATH_TO_NUGET = 'C:/"Program Files (x86)"/NuGet/'
        // PROJECT_NAME = 'ConsoleAppHelloWorld'
    }

    options {
            //Skip checking out code from source control by default in the agent directive.
        skipDefaultCheckout true 
            //Used with docker or dockerfile top-level agent. 
            //When specified, each stage will run in a new container instance on the same node, rather than all stages running in the same container instance.
        	// newContainerPerStage false
    }

    stages {

    	// agent { 
    	// 	label 'gcloud-slave'
    	// 	// node { label 'gcloud-slave' }
    	// }

    	stage('Checkout') {
      		checkout scm
      		echo "Hello!"
      		sh sleep 1
    	}

   //  	stage('Environment') {
			// sh 'git --version'
			// echo "Branch: ${env.BRANCH_NAME}"
			// sh 'docker -v'
			// sh 'printenv'
	  //   }

	  //   stage('Build Docker test'){
			// sh 'docker build -t react-test -f Dockerfile.test --no-cache .'
	  //   }

	  //   stage('Docker test'){
			// sh 'docker run --rm react-test'
	  //   }

	  //   stage('Clean Docker test'){
			// sh 'docker rmi react-test'
	  //   }

	  //   stage('Deploy'){
			// if(env.BRANCH_NAME == 'master') {
			// 	sh 'docker build -t react-app --no-cache .'
			// 	sh 'docker tag react-app localhost:5000/react-app'
			// 	sh 'docker push localhost:5000/react-app'
			// 	sh 'docker rmi -f react-app localhost:5000/react-app'
	  //     	}
	  //   }


    }

    post {
        always {
            echo 'Post message'
        }
        failure {
            echo 'On Failure post-condition'
        }
        success {
            echo 'On Success post-condition'
        }
        cleanup {
            deleteDir()
        }
    }


}