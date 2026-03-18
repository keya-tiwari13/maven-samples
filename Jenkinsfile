pipeline {
  agent any
  tools {
    maven 'DHT_MVN'
    jdk 'DHT_SENSE'
  }

  stages {
    stage('check out') {
      steps {
        git(url: 'https://github.com/keya-tiwari13/maven-samples-A6.git', branch: 'master')
      }
    }

    stage('git bisect') {
      steps {
        sh '''
          set +e

          git bisect reset || true
          git bisect start

          git bisect good 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5
          git bisect bad 198644632661c67b6c32f59e9047c11a70685e15

          git bisect run mvn verify

          RESULT=$?

          echo "First bad commit found:"
          git bisect log

          git bisect reset
          exit $RESULT
        '''
      }
    }
  }
}
