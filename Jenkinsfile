pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                  ls -lah > app.sh
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                  cat ./app.sh
                '''
            }
        }
        stage('Prod'){
            steps {
                input message: "deploy to prod?"
                sh '''
                  app_lines=`cat app.sh | wc -l`
                  cov_lines=`cat ${BUILD_ID}.cov | wc -l`
                  echo The app has `expr $app_lines - $cov_lines` lines uncovered > ${BUILD_ID}.rpt
                  cat ${BUILD_ID}.rpt
                  echo "We are in build ${currentBuild.number}"
                  echo "Our current result is ${currentBuild.currentResult}"      
                '''
                archiveArtifacts "${env.BUILD_ID}.rpt"
            }
        }
    }
}
