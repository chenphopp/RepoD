pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/chenphopp/grpc.git',
                    branch: 'master',
                    credentialsId: 'github-pat' 
            }
        }

        stage('Generate Doxygen Config') {
            steps {
                bat '"C:\\Program Files\\doxygen\\bin\\doxygen" -g Doxyfile'
                bat 'powershell -Command "(Get-Content Doxyfile) -replace \'^INPUT.*\', \'INPUT = src\' | Set-Content Doxyfile"'
                bat 'powershell -Command "(Get-Content Doxyfile) -replace \'^RECURSIVE.*\', \'RECURSIVE = YES\' | Set-Content Doxyfile"'
                bat 'powershell -Command "(Get-Content Doxyfile) -replace \'^GENERATE_LATEX.*\', \'GENERATE_LATEX = NO\' | Set-Content Doxyfile"'
                bat 'powershell -Command "(Get-Content Doxyfile) -replace \'^GENERATE_HTML.*\', \'GENERATE_HTML = YES\' | Set-Content Doxyfile"'
            }
        }

        stage('Run Doxygen') {
            steps {
                bat '"C:\\Program Files\\doxygen\\bin\\doxygen" Doxyfile'
            }
        }

        stage('Archive docs') {
            steps {
                bat 'tar -czf doc.tar.gz html'
                archiveArtifacts artifacts: 'doc.tar.gz', fingerprint: true
            }
        }
    }
}
