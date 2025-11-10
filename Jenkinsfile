pipeline {
    agent any

    environment {
        REPORT_DIR = "/tmp/runtime_results"
        FINAL_DIR = "/tmp/final_reports"
    }

    stages {

        stage('Run JMeter Test') {
            steps {
                sh '''
                echo "🚀 Starting JMeter Test Execution..."
                mkdir -p $REPORT_DIR && chmod -R 777 $REPORT_DIR

                # Remove old reports
                rm -rf $REPORT_DIR/report

                # Run JMeter
                jmeter -n -t /P01_HTTPBinAPI_StreeTest.jmx -l $REPORT_DIR/results.jtl -e -o $REPORT_DIR/report

                echo "✅ JMeter test completed"
                '''
            }
        }

        stage('Collect Reports') {
            steps {
                sh '''
                echo "📦 Collecting JMeter report and cAdvisor metrics..."
                mkdir -p $FINAL_DIR && chmod -R 777 $FINAL_DIR

                # Copy JMeter HTML report
                if [ -d "$REPORT_DIR/report" ]; then
                    cp -r $REPORT_DIR/report $FINAL_DIR/JMeter-Report
                    echo "✅ JMeter HTML report copied."
                else
                    echo "⚠️ No JMeter report found."
                fi

                # Copy cAdvisor metrics
                curl -s http://localhost:8080/metrics > $FINAL_DIR/cadvisor_metrics.txt || echo "⚠️ Skipped cAdvisor metrics."
                '''
            }
        }

        stage('Publish HTML Report') {
            steps {
                publishHTML(target: [
                    allowMissing: true,
                    keepAll: true,
                    reportDir: "${FINAL_DIR}/JMeter-Report",
                    reportFiles: 'index.html',
                    reportName: 'JMeter HTML Report'
                ])
            }
        }
    }

    post {
        always {
            echo "🏁 Pipeline completed."
        }
    }
}
