Here i've created a simple AWS CICD automation by using the below AWS tools

CodeCommit
CodeBuild
CodePipeline  
Elastic Container Registry
Elastic Container service
S3 to store the artifacts


The basic idea behind the project, once the developer did the code changes and pushed to the Code commit Repo it will trigger and build the corresponding Docker image and store the artifacts into the S3 and also pushed the image to the ECR that we have used for our container registry.
Stages that we are using here for Build and Deploy.

Once the build has been completed,  deployment will be happening in the ECS(Elastic Container Service) behind the Loadbalancers.

Steps:
1. Setting up CodeCommit (Private Code Repository) and create Security Credentials Dashboard and create “HTTP Git credentials for AWS CodeCommit”, save it.
2. Clone the repository to your local machine and when asked for credentials use the creds which we saved in the above step.
3. Add, commit and push some changes and make sure you can see these files in your CodeCommit Repo.
4. Creating a project in CodeBuild
5. Environment variable that we have used here,
   AWS_DEFAULT_REGION with a value of us-west-2(use your region).
   AWS_ACCOUNT_ID with a value of your Account ID.
   IMAGE_TAG with a value of latest
   IMAGE_REPO_NAME (ECR repo name)
6. Navigate to ECR and create a private repository.
7. Also Navigate to IAM ➡ Roles. Search for the role that was created while configuring CodeBuild.
8. Attach the policy “AmazonEC2ContainerRegistryPowerUser” to the role
9. Go to the CodeBuild and run the Build and under the Phase detailstab you can see the build status of each step.
10. And after the successfull run, we can see the corresponding Docker image in the ECR repo.
11. Navigate to CodePipeline ➡ Create a new pipeline.
12. Once the pipeline has created and before adding deploy stage, Create a cluster in Amazon ECS and Service
13. Create and configure ECS service, Task defenition and Services.
14. Then create a Deploy stage in Codepipeline and choose Amazon ECS as Action provider.
15. Choose BuildArtifact as Input artifact.
16.It alls done, if we make any small changes and push to repo it will trigger the pipeline and deploying to the ECS.
17. We can test it by using the public IPv4 that will get it from the ECS task




   
