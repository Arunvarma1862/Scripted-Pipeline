node('built-in'){
    stage('Continous Download')
    {
        git branch: 'main', url: 'https://github.com/Arunvarma1862/maven-tomcat.git'
    }
    stage('Continous Build')
    {
        sh 'mvn package'
    }
    stage('Continous Delivery')
    {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat9', path: '', url: 'http://172.31.14.49:8080')], contextPath: 'testapps', war: '**/*.war'
    }
    stage('Continous Testing')
    {
        git branch: 'main', url: 'https://github.com/Arunvarma1862/Functional-Testing.git'
        sh 'java -jar /var/lib/jenkins/workspace/Scripted-Pipeline/testing.jar'
    }
    stage('Continous Deploy')
    {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatProd', path: '', url: 'http://172.31.0.224:8080')], contextPath: 'prodapps', war: '**/*.war'
    }
}
