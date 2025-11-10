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
                bat '"C:\\Users\\sreek\\Desktop\\apache-jmeter-5.6.3\\bin\\jmeter.bat" -n -t P01_HTTPBinAPI_StreeTest.jmx -l Results\\results.jtl -e -o Results\\report'
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: 'Results\\report\\**', fingerprint: true
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
