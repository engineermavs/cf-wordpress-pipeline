@Library('shared-library') _
pipeline {
    agent any
	
	environment {
	AWS_CRED = 'cloud_user'
        AWS_REGION = 'us-east-1'	
      	bucketName = "testbucket-mavs"
	stackFileName = "wordPress.yaml"
	VpcId = "vpc-053b338aed86f79f5"
	PubSub1 = "subnet-0d918b2afdb1a9bea"
	PubSub2 = "subnet-004cd798e13e870d0"
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
				uploadFiles(stackFileName: "${stackFileName}", workingDir: "${env.WORKSPACE}/stack-templates", bucketName: "${bucketName}")
			}
		}
		stage('Deploy Stack') {                  
                steps {
                    deployStack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}", VpcId: "${VpcId}", PublicSubnet1: "${PubSub1}", PublicSubnet2: "${PubSub2}")
                }
            }
		
		  
    }
   }
