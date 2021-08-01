# Rolling Update In AWS ECS

1. What is the rolling update in AWS ECS?

   - In a rolling update, the Amazon ECS service scheduler swap the currently running tasks with new tasks. The number of tasks that Amazon ECS adds or removes from the service during a rolling update is managed by the deployment configuration. The deployment configuration consists of the minimumHealthyPercent and maximumPercent, both of these values are very important to ensure an ECS task is up & running during updates.

   - The minimumHealthyPercent represents the lower limit on the number of tasks that should be running for a service during a deployment or when a container instance is draining, as a percent of the desired number of tasks for the service

   - The maximumPercent represents the upper limit on the number of tasks that should be running for a service during a deployment or when a container instance is draining, as a percent of the desired number of tasks for a service.


2. Demo Blog <a href="https://sanchitdilipjain.github.io/rolling-update-in-ecs/">link
