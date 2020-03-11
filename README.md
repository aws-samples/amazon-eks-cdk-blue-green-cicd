## Building CI/CD with Blue/Green and Canary Deployments on EKS using CDK

In this workshop you'll learn how to build a CI/CD pipeline (AWS CodePipeline) to develop a web-based application, containerize it, and deploy it on a Amazon EKS cluster. You'll use the blue/green method to deploy application and review the switchover using Application Load Balancer (ALB) Target-groups. You will spawn this infrastructure using AWS Cloud Development Kit (CDK), enabling you to reproduce the environment when needed, in relatively fewer lines of code.

The hosting infrastructure consists of pods hosted on Blue and Green service on Kubernetes Worker Nodes, being accessed via an Application LoadBalancer. The Blue service represents the production environment accesssed using the ALB DNS with http query (group=blue) whereas Green service represents a pre-production / test environment that is accessed using a different http query (group=green). The CodePipeline build stage uses CodeBuild to dockerize the application and post the images to Amazon ECR. In subsequent stages, the image is picked up and deployed on the Green service of the EKS. The Codepipeline workflow is then blocked at the approval stage, allowing the application in Green service to be tested. Once the application is confirmed to be working fine, the user can issue an approval at the Approval Stage and the application is then deployed on to the Blue Service.

The CodePipeline would look like the below figure:

<img src="images/stage12-green.png" alt="dashboard" style="border:1px solid black">
<img src="images/stage34-green.png" alt="dashboard" style="border:1px solid black">

The current workshop is based upon this link and the CDK here is extended further to incorporate CodePipeline, Blue/Green Deployment on EKS with ALB. We will also use the weighted target-group to configure B/G Canary Deployment method. Note that currently CodeDeploy does not support deploying on EKS and thus we will instead use CodeBuild to run commands to deploy the Containers on Pods, spawn the EKS Ingress controller and Ingress resource that takes form of ALB. This workshop focuses on providing a simplistic method, though typical deployable model for production environments. Note that blue/green deployments can be achieved using AppMesh, Lambda, DNS based canary deployments too.



## License

This library is licensed under the MIT-0 License. See the LICENSE file.

