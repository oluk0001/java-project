properties([pipelineTriggers([githubPush()])])
node('linux'){
    stage('Test'){
        git 'https://github.com/oluk0001/java-project.git'
        sh 'ant -f test.xml -v'
    }
    stage('Build'){
        sh 'ant -f build.xml -v'
    }
    stage('Results'){
		sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
	    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '276e9e6d-aa56-44c3-98c4-332f143ce90a', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
        {
    // some block
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'
        }
    }
}
