node('built-in') {

    stage('Continuous Download') {
        try {

            git branch: 'main',
                url: 'https://github.com/Arunvarma1862/maven-tomcat.git'

            echo "Source Code Downloaded Successfully"

        } catch (Exception e) {

            echo "Continuous Download Stage Failed"

            mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Pipeline Stopped Due to Download Failure")
        }
    }

    stage('Continuous Build') {
        try {

            sh 'mvn clean package'

            echo "Build Completed Successfully"

        } catch (Exception e) {

            echo "Continuous Build Stage Failed"

           mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Pipeline Stopped Due to Build Failure")
        }
    }

    stage('Continuous Delivery') {
        try {

            deploy adapters: [
                tomcat9(
                    alternativeDeploymentContext: '',
                    credentialsId: 'Tomcat9',
                    path: '',
                    url: ''http://172.31.14.49:8080'
                )
            ],
            contextPath: 'testapp',
            war: '**/*.war'

            echo "Application Deployed to Test Server Successfully"

        } catch (Exception e) {

            echo "Continuous Delivery Stage Failed"

             mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Pipeline Stopped Due to Delivery Failure")
        }
    }

    stage('Continuous Testing') {
        try {

            git branch: 'main',
                url: 'https://github.com/Arunvarma1862/Functional-Testing.git'

            sh 'java -jar /var/lib/jenkins/workspace/Scripted-Pipeline/testing.jar'

            echo "Functional Testing Completed Successfully"

        } catch (Exception e) {

            echo "Continuous Testing Stage Failed"
   mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Pipeline Stopped Due to Testing Failure")
        }
    }

    stage('Continuous Deploy') {
        try {

            deploy adapters: [
                tomcat9(
                    alternativeDeploymentContext: '',
                    credentialsId: 'tomcatProd',
                    path: '',
                    url: http://172.31.0.224:8080'
                )
            ],
            contextPath: 'prodapp',
            war: '**/*.war'

            echo "Application Deployed to Production Successfully"

        } catch (Exception e) {

            echo "Continuous Deploy Stage Failed"

           mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Pipeline Stopped Due to Production Deployment Failure")
        }
    }
}
