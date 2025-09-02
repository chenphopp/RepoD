pipeline {
    agent any
    stages {
        stage('Checkout RepoA') {
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
                bat 'powershell -Command "(Get-Content Doxyfile) -replace \'^WARN_LOGFILE.*\', \'WARN_LOGFILE = warnings.log\' | Set-Content Doxyfile"'
            }
        }

        stage('Run Doxygen with Warnings') {
            steps {
                bat '"C:\\Program Files\\doxygen\\bin\\doxygen" Doxyfile'
            }
        }

        stage('Checkout RepoC') {
            steps {
                git url: 'https://github.com/chenphopp/RepoC.git',
                    branch: 'main',
                    credentialsId: 'github-pat'
            }
        }

        stage('Run Parser') {
            steps {
                bat '"C:\\Users\\chenp\\AppData\\Local\\Programs\\Python\\Python313\\python" log_parser.py warnings.log'
                archiveArtifacts artifacts: 'warnings.csv', fingerprint: true
            }
        }
    }
}
