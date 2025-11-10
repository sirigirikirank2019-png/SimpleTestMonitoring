pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/sirigirikirank2019-png/SimpleTestMonitoring.git', branch: 'main'
            }
        }

        stage('Setup JMeter') {
            steps {
                // Adjust path if JMeter is already installed
                bat 'echo JMeter path: C:\\Users\\sreek\\Desktop\\apache-jmeter-5.6.3\\bin'
            }
        }

        stage('Run JMeter Test') {
            steps {
                bat '"C:\\Users\\sreek\\Desktop\\apache-jmeter-5.6.3\\bin\\jmeter.bat" -n -t P01_HTTPBinAPI_StreeTest.jmx -l C:\\Users\\sreek\\Desktop\\Jmeter_Scripts\\Results\\results.jtl -e -o C:\\Users\\sreek\\Desktop\\Jmeter_Scripts\\Results\\report'
            }
        }

        stage('Collect Reports') {
            steps {
                bat 'mkdir final_reports'
                bat 'xcopy /E /I report final_reports\\JMeter-Report'
                echo '✅ Reports collected'
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: 'final_reports/**', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
