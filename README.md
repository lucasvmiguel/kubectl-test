# kubectl-test

A kubectl plugin to run integration tests in a kubernetes cluster, the job status is going to be used to define if a test has passed or not. To create a new test it is required to create at least one job with a label: type=test (label can be modified)

Reference: https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/

## Requirements

| Name    | Website                                                 |
| ------- | ------------------------------------------------------- |
| jq      | https://stedolan.github.io/jq/                          |
| kubectl | https://kubernetes.io/docs/tasks/tools/install-kubectl/ |

## Install

```bash
git clone https://github.com/lucasvmiguel/kubectl-test.git
cd kubectl-test
chmod +x ./kubectl-test
cp kubectl-test /usr/local/bin
```

## Usage

```bash
A kubectl plugin to run integration tests in a kubernetes cluster,
the job status is going to be used to define if a test has passed or not.
To create a new test it is required to create at least one job with a label:


  Usage:
    kubectl test <action>

  Targets:
    kubectl test --help             Show help command
    kubectl test check              Check if the tests were successfull
    kubectl test cleanup            Remove all test resources from the cluster
```

## Test case

```yml
apiVersion: batch/v1
kind: Job
metadata:
  name: job-success
  labels:
    type: test
spec:
  template:
    spec:
      containers:
        - name: main
          image: bash
          command: ["/bin/bash", "-c", "sleep 10 && exit 0"]
      restartPolicy: Never
```
