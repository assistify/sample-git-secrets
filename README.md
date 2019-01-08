# Never publish your secrets to git - anymore

## [tl:dr] 

```
npm i && echo 'AWS_SECRET_KEY = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEZ' >foo.txt && git add foo.txt && git commit -m "publish aws key"
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

## What git secrets is about

[Git secrets](https://github.com/awslabs/git-secrets) is a utility extending the git bash: It checks the content of the git repository and validates that password/credential patterns are not contained.

If you ever published your AWS secret key by accident to Github you know you missed such a feature

## Caveats

- Git secrets needs to be installed on your local machine (you need to do this yourself once)
- In order to be effective, a pre-commit-hook needs to be created. Depending on your programming language and toolchain, there might be mechanisms how to distribute the hook. This repository contains a working sample for Node.js (NPM)
