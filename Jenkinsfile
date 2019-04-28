properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Build'){
        git 'https://github.com/ccollins12000/java-project.git'
        sh "ant -f build.xml -v"
    }
    
    stage('Test'){
        sh "ant -buildfile test.xml"
    }
    
    stage('Reports'){
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh 'aws cloudformation describe- stack-resources --region us-east-1 --stack-name jenkins'
        }
    }
}
