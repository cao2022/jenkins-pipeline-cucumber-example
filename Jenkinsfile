pipeline{

    agent any
    environment{
        REPORT_PATH = "${env.WORKSPACE}/../builds/${BUILD_NUMBER}/cucumber-html-reports/overview-features.html"
    }
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
        print "${env.REPORT_PATH}"
        emailext attachLog: true, body: '${FILE, path=${env.REPORT_PATH}}', mimeType: 'text/html', subject: 'cucumber-report', to: '1520413997@qq.com'
      }
    }
}