node('built-in') {
    stage('Codecheckout')
{
    git 'https://github.com/Levisngakop/maven.git'
}
  stage('Codebuild')
{
    sh 'mvn package'
} 
stage('CodedeployQAT') 
{
    deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://4.227.254.138:8083/testapp')], contextPath: 'testapp', war: '**/*.war'
}
stage('Codetesting') 
{
    git 'https://github.com/Levisngakop/testingproject.git'
    sh 'java -jar /var/lib/jenkins/workspace/levis-pipeline/testing.jar'
}
stage('CodedeployPROD') 
{
    deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://4.227.254.138:8083/webapp')], contextPath: 'webapp', war: '**/*.war'
}
}
