# CI/CD

- CodeCommit
- CodeBuild
- CodeDeploy
	- In-Place
	- Blue/Green
- CodePipeline (integrates with all of the above)
	- Integrations
		- CodeCommit, CodeBuild, CodeDeploy
		- GitHub
		- Jenkins
		- EB
		- CloudFormation
		- Lambda
		- ECS

In-Place
- Capacity is reduced during the deployment
- Lambda not supported
- Rolling back = redeploy
- Good for first time deployment

Blue/Green
- No capacity reduction
- Green instances can be created ahead of time
- Easy to switch between old and new
- You pay for 2 environments until you terminate the old servers

AppSpec File
- Configuration file
	- Defines params used in deployment
- EC2
	- EC2 & on-premises
	- YAML
- Lambda
	- YAML / JSON
	- File structure depends on Lambda/EC2

File structure (/appspec.yml)
- Version
- OS
- Files
- Hooks

Scripts you might run during deployment
- Unzip files
- Run tests
- Deal with load balancing

Phases of Lifecycle Hooks
- Phase 1: De-register instances from a Load Balancer
	- BeforeBlockTraffic
	- BlockTraffic
	- AfterBlockTraffic
- Phase2: The real nuts & bolts of the application deployment
	- ApplicationStop
	- DownloadBundle
	- BeforeInstall
	- Install
	- AfterInstall
	- ApplicationStart
	- ValidateService
- Phase3: Re-register instances with the Load Balancer
	- BeforeAllowTraffic
	- AllowTraffic
	- AfterAllowTraffic


## CodeArtifact

An artifact repository that makes it easy for developers to find the software packagess they need

- Artifact repository: Securely store, publish and share
- Software packages: bundle of software
- Including Open-Source
	- Curate approved packages






---

