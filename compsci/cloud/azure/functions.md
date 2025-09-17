---
tags: cloud
---

### azure functions and server less computing
- is an event-driven, server-less compute option that doesn't require maintaining virtual machines or containers

- if you build an app using VMs or containers, those resources have to be "running" in order for your app to function... events wake the azure function, alleviating the need to keep resources provisioned when there are no events

### benefits of azure functions
- ideal when you are only concerned about the code running your service and not about the underlying platform or infrastructure

- functions can either be...
  
  1. stateless - the functions behave as if they restart every time they respond to event

  2. stateful - context is passed through the function to track prior activity