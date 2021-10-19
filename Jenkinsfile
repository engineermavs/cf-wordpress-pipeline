@Library('shared-library') _
pipeline {
    agent any
	
	environment {
	AWS_CRED = 'cloud_user'
        AWS_REGION = 'us-east-1'	
      	bucketName = "testbucket-mavs"
	stackFileName = "wordPress.yaml"
    }
	
	parameters { 
		string(
			name: 'ENV', 
			defaultValue: 'DEV', 
			description: 'Please insert the environment'
			)
		string(
			name: 'stackName', 
			defaultValue: 'myStack-mavs', 
			description: 'Please insert the stack name'
			)
	}
	
    stages {
     
		stage("Push template to S3") {
			steps {
				uploadFiles(stackFileName: "${stackFileName}", workingDir: "${env.WORKSPACE}/stack_templates", bucketName: "${bucketName}")
			}
		}
		stage('Deploy Stack') {                  
                steps {
                    deployStack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}")
                }
            }
		
		  
    }
   }
