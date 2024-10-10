# policy-exceptions-demo
There are two ways to manage Policy Exceptions in NPM.
* Deploy via NPM
* Deploy via GitOps

This is a demo repository for deploying and managing Policy Exceptions with GitOps.

>Note: Detailed steps can be found on the [official docs site](https://docs.nirmata.io/docs/npmk/policy_exceptions/gitops-deployment/).

## Policy Exceptions
Policy Exceptions are temporary deviations that are required when following the policy practices might not be possible because it can hinder operational needs.

## Policy Exception Request and Approval
Every policy exception request is sent to an admin for review. The admin can either accept or reject the request. If the request gets accepted, the PolicyException resource gets deployed and the user who requested the exception gets notified via email.

More details on the exception request and approval process [here](https://docs.nirmata.io/docs/npmk/policy_exceptions/#policy-exception-workflow).

## GitOps for Policy Exception Deployment
Once the PolicyException Request is approved in NPM, you can use [nctl](https://docs.nirmata.io/docs/nctl/getting-started/) to create Pull Requests (PRs) to relevant repositories.

Here are some useful commands.

View all requests.
```sh
nctl get policyexceptionrequest
```

To create PRs for all **approved** exception requests, run the following command.
```sh
nctl create pull-request
```

>Note: See sample PRs in this repo to get an idea of what a PolicyException PR looks like.

To create a PR for a specific exception request (it has to be approved), run the following command.
```sh
nctl create pull-request --per-name <per-name>
```

Now the PR is created and can be reviewed by other team members. Once the PR is merged, your GitOps tool will deploy the PolicyException resource to target environments.

NPM highlights the different states of your PR and ultimately detects when the resource is deployed in the clusters. It also correlates the approved exceptions with the resources deployed by the GitOps tool, and flags any unknown exceptions.
