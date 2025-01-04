## Jenkins Job Builder action

This action launches [Jenkins Job Builder](https://jenkins-job-builder.readthedocs.io/en/latest/) to update your Jenkins jobs.

## Example

```yaml
name: jjb

on:
  push:
    paths:
      - jenkins/jobs/**                             # job definitions here, searched recursively

jobs:
  jjb:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: devopsx/action-jjb@master
        with:
          jjb_user: ${{ vars.JJB_USER }}
          jjb_password: ${{ secrets.JJB_PASSWORD }}
          jjb_dir: jenkins/jobs                      # Same dir with definitions as in push stanza
          jjb_ini: jenkins/jenkins_jobs.ini          # See example
```

## Configuration

1. Create a dedicated github account in Jenkins, and an [API token](https://www.jenkins.io/blog/2018/07/02/new-api-token-system/) for it.
2. Create `JJB_USER` variable (account from step 1) and `JJB_PASSWORD` (token from step 1) [secret](https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository) in repository settings.
3. Add workflow yaml, as described above.

That's it!
