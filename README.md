# kojo-test


For the github pipeline you have to mention below:
<AWS_ACCOUNT_ID>            Your AWS account ID
<GITHUB_ACTIONS_EKS_ROLE>   IAM Role name for GitHub OIDC
<AWS_REGION>                E.g., us-west-2
<EKS_CLUSTER_NAME>          Name of your EKS cluster




OIDC for integrating it with AWS with github=>

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Federated": "arn:aws:iam::<AWS_ACCOUNT_ID>:oidc-provider/token.actions.githubusercontent.com"
      },
      "Action": "sts:AssumeRoleWithWebIdentity",
      "Condition": {
        "StringLike": {
          "token.actions.githubusercontent.com:sub": "repo:<OWNER>/<REPO>:ref:refs/heads/release/*"
        }
      }
    }
  ]
}