pipeline {
  agent {
    kubernetes {
      inheritFrom 'cob'
      yaml '''
      spec:
        volumes:
        - name: docker-socket
          emptyDir: {}
        containers:
        - name: gradle
          image: gradle:7.1.1-jdk-11
          command:
            - cat
          tty: true
        - name: docker
          image: docker:19.03.1
          command:
          - sleep
          args:
          - 99d
          volumeMounts:
          - name: docker-socket
            mountPath: /var/run
        - name: docker-daemon
          image: docker:19.03.1-dind
          securityContext:
            privileged: true
          volumeMounts:
          - name: docker-socket
            mountPath: /var/run

    '''
    }
  }
  stages {
    stage ('Git check out') {
      steps {
        git
      }
    }
  }
}
