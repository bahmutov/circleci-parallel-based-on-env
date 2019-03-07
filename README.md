# circleci-parallel-based-on-env [![CircleCI](https://circleci.com/gh/bahmutov/circleci-parallel-based-on-env.svg?style=svg)](https://circleci.com/gh/bahmutov/circleci-parallel-based-on-env)

CircleCI cannot vary `parallelism` parameter based on environment variable. But you can define different jobs (or even a single job with a parameter), and pick one to run based on branches, see [config docs](https://circleci.com/docs/2.0/configuration-reference/#jobs-1)

To see effective config

```shell
circleci config process circle.yml | sed /^#/d
```

So we do the following: in the workflow we call same job depending on the branch filters, and we pass a parameter to the job to control `parallelism`.

- if this is a `master` or internal branch and internal pull request, the branch name will be whatever you set it to.
- if pull request is coming from external forked branch, then the branch will be named `pull/<number>`

See [circle.yml](circle.yml) and compare the runs

- master branch [on two machines](https://circleci.com/workflow-run/39e20855-191d-4da2-8171-675c90e97175)
- internal branch [on two machines](https://circleci.com/workflow-run/b06a7547-b0a1-40d5-aba4-15d154a3657a)
- external pull request from a forked repo [on one machine](https://circleci.com/workflow-run/3f4acfba-e23a-4d77-bb03-a59b4162bc95)
