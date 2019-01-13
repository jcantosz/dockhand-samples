@Library('dockhand@sample')
import com.boxboat.jenkins.pipeline.build.*

def build = new BoxBuild()

node() {
  build.wrap {
    stage('Build'){
      build.composeBuild("dev")
    }
    stage('Run'){
      build.composeUp("dev")
    }
    stage('Test'){
      sh """
        HOST=\$(docker container port nginx-sample 80 | sed 's/0\\\\.0\\\\.0\\\\.0/localhost/g')
        curl $HOST
      """
    }
    stage('Teardown'){
      build.composeDown("dev")
    }
  }
}
