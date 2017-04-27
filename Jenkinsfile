node {
    checkout scm
    def is_pr = env.JOB_NAME.endsWith("_pull-requests");
//    setGitHubPullRequestStatus state: 'PENDING', context: "${env.JOB_NAME}", message: "Run #${env.BUILD_NUMBER} started";

    //works but [Set GitHub commit status (universal)] PENDING on repos [] (sha:5152281) with context:jenkins-test
    step([$class: 'GitHubCommitStatusSetter', contextSource: [$class: 'ManuallyEnteredCommitContextSource', context: 'jenkins-test']])

    step([$class: 'GitHubSetCommitStatusBuilder', statusMessage: [content: 'Pending sleep']])
}
