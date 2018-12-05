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
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIAJRHI6GTRT522YUFA', credentialsId: '', secretKeyVariable: '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']])
	{
    // some block
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'
        }
 stage('Deploy'){
	sh "aws s3 cp $OUTPUT/target/foo-bar.jar s3://seis66510assign/${env.BRANCH_NAME}/"
	}  
    }
}



