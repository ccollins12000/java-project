properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Unit Tests'){
        git 'https://github.com/ccollins12000/java-project.git'
        sh "ant -f test.xml -v"
        junit 'reports/result.xml'
    }
    stage('Build'){
        git 'https://github.com/ccollins12000/java-project.git'
        sh "ant -f build.xml -v"
    }
    stage('Deploy'){
        sh "echo ${BUILD_NUMBER}"
    }
    
    stage('Reports'){
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins-stack'
        }
    }
}
