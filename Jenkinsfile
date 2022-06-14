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
        def report_path = report_path()
        emailext attachLog: true, body: '${FILE, path=report_path}', mimeType: 'text/html', subject: 'cucumber-report', to: '1520413997@qq.com'
      }
    }
}

def report_path(){
    def report_path = "${env.WORKSPACE}/../builds/${BUILD_NUMBER}/cucumber-html-reports/overview-features.html"
    print report_path
    return report_path
}