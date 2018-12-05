properties([pipelineTriggers([githubPush()])])
node('linux'){
    stage('Test'){
        git 'https://github.com/oluk0001/java-project.git'
        sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
    }
    stage('Build'){
        sh 'ant -f build.xml -v'
    }
   stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '1b10528c-592e-4765-8688-79017ee19e64', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
        {
    // some block
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'
        }
 stage('Deploy') 
  {
sh ("aws s3 cp $WORKSPACE s3://seis66510assign/${JOB_NAME}/${BUILD_NUMBER}/ --recursive --exclude '*' --include '*.jar'")
	}
    }
}

