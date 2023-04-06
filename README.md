# Bringing Media2Cloud Video Analysis into Amazon Neptune Knowledge Graph

This is an example accompanying my blog post on linking AI video analysis of the AWS Media2Cloud solution (https://aws.amazon.com/solutions/implementations/media2cloud/) with an Amazon Neptune knowledge graph. Refer to the blog post for a full step-to-step setup and exploration.

We refer to Media2Cloud as M2C throughout.

## Pre-requisite
To run this example, you need an AWS account with permission to create resources such as a Neptune cluster and M2C.

You will be provisioning resources in one AWS Region. You must choose a Region supported by both Neptune (https://docs.aws.amazon.com/neptune/latest/userguide/get-started-cfn-create.html) and M2C (https://docs.aws.amazon.com/solutions/latest/media2cloud-on-aws/deployment-considerations.html). 

## Steps to setup
### Setup M2C
Create M2C by launching its AWS CloudFormation stack. For instructions, refer to Launch the stack (https://docs.aws.amazon.com/solutions/latest/media2cloud-on-aws/automated-deployment.html#step-1.-launch-the-stack). When it’s complete, you receive an email (to the address you specified as a parameter to the stack) with instructions to log in to the M2C portal. Confirm you can access the portal. 

Additionally, obtain the name of the S3 analysis bucket that M2C creates. On the AWS CloudFormation console, find the stack whose name contains CoreStack. On the Outputs tab of that stack, copy the value of the output ProxyBucket. 

### Upload videos to M2C
Upload your videos, or videos from a third party (complying with their usage rules). Wait for the ingest and analysis processing to complete. See the blog post for more.

### Set up a Neptune cluster and notebook
In the same Region in which you installed M2C, create Neptune resources using 
using AWS CloudFormation. First download a copy of the CloudFormation template (cfn/NepM2CStack.yaml). Then complete the following steps:

1.	On the AWS CloudFormation console, choose Create stack.
2.	Choose With new resources (standard).
3.	Select Upload a template file.  
4.	Choose Choose file to upload the local copy of the template that you downloaded. The name of the file is NepM2C.yaml.
5.	Choose Next.
6.	Enter a stack name of your choosing. 
7.	In the Parameters section, enter a value for M2CAnalysisBucket. Use the value collected after setting up M2C. Use defaults for the remaining parameters.
8.	Choose Next.
9.	Continue through the remaining sections.
10.	Read and select the check boxes in the Capabilities section.
11.	Choose Create stack.
12.	When the stack is complete, navigate to the Outputs section and follow the link for the output NeptuneSagemakerNotebook. This opens in your browser the Jupyter files view.
13.	In Jupyter, select M2CForKnowledgeGraph.ipynb to open the notebook that use you in the remaining steps.

We encourage you to review the stack with your security team prior to using it in a production environment.

Setup steps are discussed in detail in the blog post.

## Cost
Running this example incurs charges. M2C has both one-time costs for processing of ingest and analysis, plus recurring costs for S3 storage, portal, and search engine. Refer to the M2C cost guide (https://docs.aws.amazon.com/solutions/latest/media2cloud-on-aws/cost.html). Neptune costs 
(https://aws.amazon.com/neptune/pricing/) include on-demand instances, storage and I/O, and workbench. Testing the five videos above results in a negligible one-time cost. However, Neptune instance costs and M2C recurring costs accumulate hourly. 

## Clean up
If you’re done with the solution and wish to avoid future charges, delete the M2C and Neptune stacks. 
## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

