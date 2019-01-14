node('ephemeral-slave') {

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

    stage('Build Docker test'){
      sh 'docker build -t react-test -f Dockerfile.test --no-cache . '
    }

    stage('Docker test'){
      sh 'docker run --rm react-test'
    }

    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    }

    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t react-app --no-cache .'
        
        sh 'docker tag react-app localhost:5000/react-app'
        sh 'docker push localhost:5000/react-app'
        sh 'docker rmi -f react-app localhost:5000/react-app'

        // sh 'docker tag react-app http://192.168.99.100:5000/react-app'
        // sh 'docker push http://192.168.99.100:5000/react-app'
        // sh 'docker rmi -f react-app http://192.168.99.100:5000/react-app'
      }
    }

  }

  catch (err) {
    throw err
  }

}

// node ('dockerslave') {
//     stage 'Stage 1'
//     sh 'echo "Hello from your favorite test slave!"'
//     docker.image('alpine').inside {
//         sh 'echo "hello from inside a container!"'
//     }
// }