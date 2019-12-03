# chaos toolkit-poc
my experiments with chaos toolkit poc

## Introduction to Chaos toolkit

Chaos tool kit practices chaos engineering and discovering how your system reacts following certain conditions you inject. 

By doing this in a controlled fashion, you may learn how to change the system accordingly.

## Why to use it?

Chaos Engineering is a disciplined approach to identifying failures before they become outages. 

By proactively testing how a system responds under stress, you can identify and fix failures before they end up in the news.

Chaos Engineering lets you compare what you think will happen to what actually happens in your systems. You literally “break things on purpose” to learn how to build more resilient systems.

## Different chaos toolkit extensions:

List of extensions : https://chaostoolkit.org/extensions

## Experiments:

Declare an Experiment to Observe the Weakness.

Details : https://docs.chaostoolkit.org/drivers/kubernetes/

**Steady state hypothesis:**

A Chaos Engineering experiment starts and ends with a steady-state hypothesis.

steady-state hypothesis determines where to start from and what a good baseline for your application is.

Here we assume two things:

* the services are running
* you can invoke your service.


**probe:** 

query your system’s state during the steady-state hypothesis

```json
{
         "type": "probe",
         "name": "application-must-respond-normally",
         "tolerance": 200,
         "provider": {
           "type": "http",
           "url": "http://192.168.64.6:31497",
           "timeout": 3
         }
       },
 ```

**method:** 

The method is the block which changes the conditions of our system/application.

```json
"method": [
    {
      "type": "action",
      "name": "stop-service",
      "provider": {
        "type": "python",
        "module": "chaosk8s.actions",
        "func": "kill_microservice",
        "arguments": {
          "name": "app=sample-app-deployment",
          "ns": "default",
          "label_selector": "app=sample-app-deployment"
        }
      }
    }
  ]

```

**rollback:** 

restore system to the original state.


## Creating a deployment:

```kubectl create -f deployment.yml```

## Creating a service:

Expose the deployment in order to create a service:

```kubectl expose deployment sample-app-deployment --type=NodePort```

## Access app URL:
```minikube service sample-app-deployment --url```

## Run chaos experiment:

``` chaos run experiment.json```

## Results:

```chaos report --export-format=pdf journal.json report.pdf```
