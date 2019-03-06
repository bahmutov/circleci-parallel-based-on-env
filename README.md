# circleci-parallel-based-on-env [![CircleCI](https://circleci.com/gh/bahmutov/circleci-parallel-based-on-env.svg?style=svg)](https://circleci.com/gh/bahmutov/circleci-parallel-based-on-env)

CircleCI cannot vary `parallelism` parameter based on environment variable. But you can define different jobs (or even a single job with a parameter), and pick one to run based on branches, see [config docs](https://circleci.com/docs/2.0/configuration-reference/#jobs-1)

To see effective config

```shell
circleci config process circle.yml | sed /^#/d
```

So we do the following: in the workflow we call same job depending on the branch filters, and we pass a parameter to the job to control `parallelism`. See [circle.yml](circle.yml) and compare the runs

- master branch [on two machines](https://circleci.com/gh/bahmutov/circleci-parallel-based-on-env/5)
- another branch [on one machine](https://circleci.com/gh/bahmutov/circleci-parallel-based-on-env/6)
