pipeline {
  agent any
  stages {
    stage('Log Tool Version') {
      parallel {
        stage('Log Tool Version') {
          steps {
            bat '''mvn --version
            git --version
            java -version'''
          }
        }

        stage('Check for POM') {
          steps {
            fileExists 'pom.xml'
          }
        }

      }
    }

    stage('Build with Maven') {
      steps {
        bat 'mvn compile'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'mvn compile'
      }
    }

    stage('Run Static Code Analysis') {
      steps {
        build job: static-code-analysis
      }
    }

    stage('Build Executable JAR File') {
      steps {
        build job: static-code-analysis
      }
    }    

    stage('Build Docker Image') {
      steps {
        build job: static-code-analysis
      }
    }

    stage('Software Versions') {
            steps {
                script {
                    def response = input message: 'Should we print the software  version?', 
                    parameters: [choice(choices: 'Yes\nNo', 
                    description: 'Proceed or Abort?', 
                    name: 'What to do???')]
                    
                    if (response=="Yes") {
                        bat 'mvn --version'
                        bat 'gradle --version'
                        bat 'git --version'
                    }
                }
            }
        }

    stage('Post Build Steps') {
      steps {
        writeFile(file: 'status.txt', text: 'Hey it worked!!!')
      }
    }

  }
}
