# Never publish your secrets to git - anymore

## [tl:dr]

**Prerequisites:** [git-secrets](https://github.com/awslabs/git-secrets) must be installed in your machine.

Checkout and build this node.js project: git-secrets will be set up automatically and prevent you to commit AWS secrets.

```
git clone https://github.com/assistify/sample-git-secrets.git
cd sample-git-secrets
npm i
echo 'AWS_SECRET_KEY = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEZ' >foo.txt
git add foo.txt
git commit -m "publish aws key"
```

// output
```
foo.txt:1:AWS_SECRET_KEY = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEZ

[ERROR] Matched one or more prohibited patterns

Possible mitigations:
- Mark false positives as allowed using: git config --add secrets.allowed ...
- Mark false positives as allowed by adding regular expressions to .gitallowed at repository's root directory
- List your configured patterns: git config --get-all secrets.patterns
- List your configured allowed patterns: git config --get-all secrets.allowed
- List your configured allowed patterns in .gitallowed at repository's root directory
- Use --no-verify if this is a one-time false positive
```

## With this solution it is possible to ensure that
- you cannot commit if git-secrets is not installed,
- git-secrets is automatically activated after building the project,
- the patterns for AWS secrets are added and recognized by default, and
- the patterns can easily be extended by editing the [patterns file](https://github.com/assistify/sample-git-secrets/blob/master/.git-secrets/patterns)

## What git secrets is about

[Git secrets](https://github.com/awslabs/git-secrets) is a utility extending the git bash: It checks the content of the git repository and validates that password/credential patterns are not contained.

If you ever published your AWS secret key by accident to Github you know you missed such a feature

## Caveats

- Git secrets needs to be installed on your local machine (you need to do this yourself once)
- In order to be effective, a pre-commit-hook needs to be created. Depending on your programming language and toolchain, there might be mechanisms how to distribute the hook. This repository contains a working sample for Node.js (NPM)

## References
- [What to Do If You Inadvertently Expose an AWS Access Key](https://aws.amazon.com/de/blogs/security/what-to-do-if-you-inadvertently-expose-an-aws-access-key/)
- [A Safer Way to Distribute AWS Credentials to EC2](https://aws.amazon.com/de/blogs/security/a-safer-way-to-distribute-aws-credentials-to-ec2/)
