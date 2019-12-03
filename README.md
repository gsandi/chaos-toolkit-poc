# chaos toolkit-poc
my experiments with chaos toolkit poc

## Introduction to Chaos toolkit

Chaos tool kit practices chaos engineering and discovering how your system reacts following certain conditions you inject. By doing this in a controlled fashion, you may learn how to change the system accordingly.

## Why to use it?

Chaos Engineering is a disciplined approach to identifying failures before they become outages. By proactively testing how a system responds under stress, you can identify and fix failures before they end up in the news.

Chaos Engineering lets you compare what you think will happen to what actually happens in your systems. You literally “break things on purpose” to learn how to build more resilient systems.

## Different chaos toolkit extensions:

List of extensions : https://chaostoolkit.org/extensions

## Experiments:

Declare an Experiment to Observe the Weakness.

**Steady state hypothesis:**

You can only learn if you know where you start from and what a good baseline for your application is.

Here we assume two things:

* the services are running
* you can invoke your service.


**probe:** Hypothesis check.

**method:** The method is the block which changes the conditions of our system/application.

**rollback:** restore to the original state.


## Creating a deployment:

```kubectl create -f deployment.yml```

## Creating a service:

Expose the deployment in order to create a service:

```kubectl expose deployment sample-app-deployment --type=NodePort```

## Access app URL:
```minikube service sample-app-deployment --url```


