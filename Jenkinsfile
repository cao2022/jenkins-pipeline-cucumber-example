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
        report_path()
        emailext attachLog: true, body: '${FILE, path="${WORKSPACE}/../builds/${BUILD_NUMBER}/cucumber-html-reports/overview-features.html"}', mimeType: 'text/html', subject: 'cucumber-report', to: '1520413997@qq.com'
      }
    }
}

report_path(){
    def report_path = "${WORKSPACE}/../builds/${BUILD_NUMBER}/cucumber-html-reports/overview-features.html"
    print report_path
}