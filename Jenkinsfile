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
}
