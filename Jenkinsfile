pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/sirigirikirank2019-png/SimpleTestMonitoring.git', branch: 'main'
            }
        }

        stage('Run JMeter Test') {
            steps {
                bat '"C:\\Users\\sreek\\Desktop\\apache-jmeter-5.6.3\\bin\\jmeter.bat" -n -t P01_HTTPBinAPI_StreeTest.jmx -l C:\\Users\\sreek\Desktop\\Jmeter_Scripts\\Results\\10112025\\results.jtl -e -o C:\\Users\\sreek\Desktop\\Jmeter_Scripts\\Results\\10112025\\report'
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: 'C:\\Users\\sreek\Desktop\\Jmeter_Scripts\\Results\\10112025\\report\\**', fingerprint: true
                echo '✅ JMeter report archived'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
