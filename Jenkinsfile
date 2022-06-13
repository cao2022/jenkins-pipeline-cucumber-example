pipeline{

    agent any

    stages {
        stage ('Test Stage') {
                steps {
                        sh 'mvn test'
                }
            }
        stage ('Cucumber Reports') {

            steps {
                cucumber buildStatus: "UNSTABLE",
                    fileIncludePattern: "**/cucumber.json",
                    jsonReportDirectory: 'target'
            }
        }
    }
    post {
      always {
        emailext attachLog: true, body: 'test', mimeType: 'text/html', subject: 'cucumber-report', to: '1520413997@qq.com'
      }
    }
}