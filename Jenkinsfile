void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/photobox/photobox/jenkins-test"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}


node {
    checkout scm
    def is_pr = env.JOB_NAME.endsWith("_pull-requests");
//    setGitHubPullRequestStatus state: 'PENDING', context: "${env.JOB_NAME}", message: "Run #${env.BUILD_NUMBER} started";

    //works but [Set GitHub commit status (universal)] PENDING on repos [] (sha:5152281) with context:jenkins-test
    step([$class: 'GitHubCommitStatusSetter', contextSource: [$class: 'ManuallyEnteredCommitContextSource', context: 'jenkins-test']])

    step([$class: 'GitHubSetCommitStatusBuilder', statusMessage: [content: 'Pending sleep']])

      step([$class: 'GitHubCommitStatusSetter',
            contextSource: [$class: 'ManuallyEnteredCommitContextSource',
                            context: 'Test Context'],
            statusResultSource: [$class: 'ConditionalStatusResultSource',
                                 results: [[$class: 'AnyBuildResult',
                                            message: 'test message',
                                            state: 'SUCCESS']]]])

setBuildStatus("Build complete", "SUCCESS");

//    githubNotify context: 'Notification key', description: 'This is a shorted example',  status: 'SUCCESS', credentialsId: 'github-photobox-services'
    githubNotify context: 'Notification key', description: 'This is a shorted example',  status: 'SUCCESS', credentialsId: 'global-github-pbx-test-notifications'
//    githubNotify context: 'Notification key', description: 'This is a shorted example',  status: 'SUCCESS', credentialsId: 'pbx-test-notifications', repo: 'photobox/jenkins-test'

}
