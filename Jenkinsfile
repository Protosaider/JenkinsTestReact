pipeline {

	// agent none
	// agent { label 'testslave' }
	// agent { label 'gcloud-slave' }
	agent { docker true }

    // environment {
    //     PATH_TO_PROJECT_ROOT = 'app/'
    //     // PATH_TO_MSBUILD = 'C:/"Program Files (x86)"/"Microsoft Visual Studio"/2017/Community/MSBuild/15.0/Bin/'
    //     // PATH_TO_NUGET = 'C:/"Program Files (x86)"/NuGet/'
    //     // PROJECT_NAME = 'ConsoleAppHelloWorld'
    // }

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
    		steps {
	      		checkout scm
	      		echo "Hello!"
	      		sh 'sleep 1'
      		}
    	}  	

    	stage('Environment') {
    		steps {
				sh 'git --version'
				echo "Branch: ${env.BRANCH_NAME}"
				sh 'docker -v'
				sh 'printenv'
			}
	    }

	    stage('Build Docker test') {
			steps {
				sh 'journalctl -u docker'
				sh 'ls -al /var/run/'
				sh 'docker build -t react-test -f Dockerfile.test --no-cache .'
			}
	    }

	    stage('Docker test') {
	    	steps {
				sh 'docker run --rm react-test'
				// sh 'docker run --rm react-test -v /var/run/docker.sock:/var/run/docker.sock'
				// RUN usermod -a -G staff jenkins
			}
	    }

	    stage('Clean Docker test') {
	    	steps {
				sh 'docker rmi react-test'
			}
	    }

	    stage('Deploy') {
	    	steps {
	    		script {
    				if(env.BRANCH_NAME == 'master') {
						sh 'docker build -t react-app --no-cache .'
						sh 'docker tag react-app localhost:5000/react-app'
						sh 'docker push localhost:5000/react-app'
						sh 'docker rmi -f react-app localhost:5000/react-app'
	    			}			
					// withDockerRegistry([credentialsId: "", url: ""])
					// docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
			            // app.push("${env.BUILD_NUMBER}")
			            // app.push("latest")
		      	}
			}
	    }

    }

    // post {
    //     always {
    //         echo 'Post message: always'
    //     }
    //     failure {
    //         echo 'On Failure post-condition'
    //     }
    //     success {
    //         echo 'On Success post-condition'
    //     }
    //     cleanup {
    //         deleteDir()
    //     }
    // }


}