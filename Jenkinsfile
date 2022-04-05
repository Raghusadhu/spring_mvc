pipeline { 
    agent any
    tools {
        maven 'maven' 
    }
 environment {
        BRANCH = 'master'
        GIT_HUB_REPO= 'https://github.com/Raghusadhu/spring_mvc.git'
    }    
     parameters(
        choice(
        choices: ['PROD', 'QA'], 
        name: 'Server Environment'
        )
        )
      stages {
       stage('Add Config files') {
       steps {
            configFileProvider([configFile(fileId: 'MyCustom', targetLocation: '/tmp/')]) {
            // some block
            }
          }
 }
        stage('clone') {
            steps {
/*           git url: 'https://github.com/Raghusadhu/spring_mvc.git' */
                git url:'${GIT_HUB_REPO}'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('code_review') {
            steps {
                sh 'mvn -P metrics pmd:pmd'
            }
        }
        stage('unit_test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('metric_check') {
            steps{
                sh 'mvn cobertura:cobertura -D cobertura.report.format=xml'
            }
        }
        stage('package') {
            steps{
                sh 'mvn package'
            }
        }
    }
}
