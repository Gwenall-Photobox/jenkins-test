node {
    checkout scm
    def is_pr = env.JOB_NAME.endsWith("_pull-requests");
    setGitHubPullRequestStatus state: 'PENDING', context: "${env.JOB_NAME}", message: "Run #${env.BUILD_NUMBER} started";
}
