void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/photobox/photobox/jenkins-test"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

def githubstatus(String context, String status, String message){
  step([$class: 'GitHubCommitStatusSetter',
      contextSource: [$class: 'ManuallyEnteredCommitContextSource', context: context],
      statusResultSource: [$class: 'ConditionalStatusResultSource',
          results: [[$class: 'AnyBuildResult', state: status, message: message]]]])
}


void setBuildStatus2(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/my-org/my-repo"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

node {
    checkout scm
    def is_pr = env.JOB_NAME.endsWith("_pull-requests");


githubNotify account: 'raul-arabaolaza', context: 'Final Test', credentialsId: 'raul-github',
    description: 'This is an example', repo: 'acceptance-test-harness', sha: '0b5936eb903d439ac0c0bf84940d73128d5e9487'    , status: 'SUCCESS', targetUrl: 'http://www.cloudbees.com'


//    setGitHubPullRequestStatus state: 'PENDING', context: "${env.JOB_NAME}", message: "Run #${env.BUILD_NUMBER} started";

    //works but [Set GitHub commit status (universal)] PENDING on repos [] (sha:5152281) with context:jenkins-test
    step([$class: 'GitHubCommitStatusSetter', contextSource: [$class: 'ManuallyEnteredCommitContextSource', context: 'jenkins-test']])

    step([$class: 'GitHubSetCommitStatusBuilder', statusMessage: [content: 'Pending sleep']])

    githubstatus('andy-githubstatus', 'SUCCESS', 'crap')

      step([$class: 'GitHubCommitStatusSetter',
            contextSource: [$class: 'ManuallyEnteredCommitContextSource',
                            context: 'Test Context'],
            statusResultSource: [$class: 'ConditionalStatusResultSource',
                                 results: [[$class: 'AnyBuildResult',
                                            message: 'test message',
                                            state: 'SUCCESS']]]])

setBuildStatus("Build complete", "SUCCESS");

sleep 30

//    githubNotify context: 'Notification key', description: 'This is a shorted example',  status: 'SUCCESS', credentialsId: 'github-photobox-services'
//    githubNotify context: 'Notification key', description: 'This is a shorted example',  status: 'SUCCESS', credentialsId: 'global-github-pbx-test-notifications'
//    githubNotify context: 'Notification key', description: 'This is a shorted example',  status: 'SUCCESS', credentialsId: 'pbx-test-notifications', repo: 'photobox/jenkins-test'

}
