node('built-in') {

    stage('Continuous Download') {
        try {

            git branch: 'main',
                url: 'https://github.com/Arunvarma1862/maven-tomcat.git'

            echo "Code Download Successfully complete "

        } catch(Exception e) {

            echo "Download Failed"

         mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Stopping Pipeline")
        }
    }

    stage('Continuous Build') {
        try {

            sh 'mvn clean package'

            echo "Build Successful"

        } catch(Exception e) {

            echo "Build Failed"

          mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Stopping Pipeline")
        }
    }

    stage('Continuous Delivery') {
        try {

            deploy(
                adapters: [
                    tomcat9(
                        credentialsId: 'tomcat9',
                      url: 'http://172.31.14.49:9001'
                    )
                ],
                contextPath: 'testapp',
                war: '**/*.war'
            )

            echo "Deployment to Test Server Successfull complete"

        } catch(Exception e) {

            echo "Delivery Failed"

          mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Stopping Pipeline")
        }
    }

    stage('Continuous Testing') {
        try {

            git branch: 'main',
               url: 'https://github.com/Arunvarma1862/Functional-Testing.git'

            sh 'java -jar /var/lib/jenkins/workspace/Scripted-Pipeline-Jenkinsfile/testing.jar'

            echo "Testing Successful"

        } catch(Exception e) {

            echo "Testing Failed"
                  mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Stopping Pipeline")
        }
    }

    stage('Continuous Deploy') {
        try {

            deploy(
                adapters: [
                    tomcat9(
                        credentialsId: 'tomcat9',
                       url: 'http://172.31.4.221:9000'
                    )
                ],
                contextPath: 'prodapp',
                war: '**/*.war'
            )

            echo "Deployment to Production Successfully "

        } catch(Exception e) {

            echo "Production Deployment Failed"
                 mail bcc: '',
                 body: "Code Download Failed\n\nError: ${e}",
                 cc: 'arunbabu1862@gmail.com',
                 from: '',
                 replyTo: '',
                 subject: 'CI/CD Pipeline Failure - Download Stage',
                 to: 'arunbabu120894@gmail.com'

            error("Stopping Pipeline")
        }
    }
}
