pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/attecius/nodejs-sample-application.git'    
		            echo "Code Checked-out Successfully!!";
            }
        }
        
        // stage('Package') {
        //     steps {
        //         sh 'mvn package'    
		//             echo "Maven Package Goal Executed Successfully!";
        //     }
        // }
        
      

	// stage('SonarQube analysis') {
    //         steps {
	// 	// Change this as per your Jenkins Configuration
    //             withSonarQubeEnv('SonarQube') {
    //                 sh 'mvn package sonar:sonar'
    //             }
    //         }
    //     }

	// stage("Quality gate") {
    //         steps {
    //             waitForQualityGate abortPipeline: true
    //         }
    //     }
	stage('script to run to have the docker image running') {
            /*when {
                expression {
                    currentBuild.result == 'SUCCESS'
                }
            }*/
            steps {
		    script {
				    sh """
				    mvn clean package
				    docker build -t webapp .
				    docker run -d -p 8081:8080 --entrypoint="/bin/sh" webapp -c "sh /usr/local/tomcat/bin/startup.sh;while true; do echo hello; sleep 10;done"
				    docker ps
				    """
                    }
                }
            }
        }
        
     
    post {
        
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    
    }
}
