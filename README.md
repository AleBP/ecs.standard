# ecs.standard
This AWS CloudFormation template is designed to set up an ECS (Elastic Container Service) infrastructure with various components and configurations.
Parameters Section
This section defines input parameters that customize the template when it is launched:

KeyPair: Specifies an existing EC2 KeyPair for SSH access.
LoadBalancerSubnets: Specifies the subnets for the load balancer.
ECSSubnets: Specifies the subnets for the ECS cluster.
VpcId: Specifies the VPC ID.
InstanceType: Defines the EC2 instance type for the ECS cluster.
DesiredCapacity: Number of instances to launch in the ECS cluster.
MinSize: Minimum number of instances in the ECS cluster.
MaxSize: Maximum number of instances in the ECS cluster.
ProyectID: An identifier for the project.
healthCheckType: Type of health check for the ALB.
LaunchTemplateVersionNumber: Version number of the launch template.
ISize: Size of the instance volume.
AmiID: Specifies the Amazon Linux AMI ID.
DNSName: Specifies a subdomain.
ACMARN: ARN of the ACM certificate.
HostedZoneId: Specifies the Route 53 Hosted Zone ID.
IntraSubnet1, IntraSubnet2, IntraSubnet3: Subnets for EFS.
ECRName: Name of the ECR repository.
Metadata Section
Organizes the parameters into groups for better readability in the CloudFormation console.

Resources Section
Defines the AWS resources to be created:

IAM Roles and Instance Profile
EC2InstanceProfile: An IAM instance profile for EC2 instances.
ContainerServiceRole: An IAM role with policies allowing ECS and other services actions.
EFS Configuration
EFSSecurityGroup: Security group for EFS.
EFSFileSystem: An EFS file system with backup enabled and encryption.
MountTarget1, MountTarget2, MountTarget3: Mount targets for EFS in different subnets.
Global Accelerator, ALB, and Security Groups
GlobalAccelerator: A Global Accelerator for improved network performance.
Listener: Listener for the Global Accelerator.
EndpointGroup: Endpoint group for the listener.
LoadBalancerSecurityGroup: Security group for the ALB.
ApplicationLoadBalancer: An ALB for distributing traffic.
HttpListenerRule: Redirects HTTP traffic to HTTPS.
HttpsListener: Listener for HTTPS traffic.
ALBTargetGroup: Target group for the ALB.
ECS Cluster, ECR Repository, and Auto Scaling
ECSCluster: An ECS cluster.
MyECRRepository: An ECR repository for storing container images.
AutoScalingGroup: An auto-scaling group for the ECS instances.
ScaleUpPolicy, ScaleDownPolicy: Policies for scaling up and down based on CPU utilization.
CPUAlarmHigh, CPUAlarmLow: CloudWatch alarms for scaling actions.
Security Groups and Launch Template
ContainerInstancesSecurityGroup: Security group for ECS instances.
LaunchTemplate: Launch template for EC2 instances with user data script for instance setup.
ECS Service and Task Definition
ECSService: An ECS service that defines the desired number of tasks, load balancer, and network configuration.
ExecutionRole, TaskRole: IAM roles for ECS task execution.
TaskDefinition: Defines the task to run in ECS, including container image, CPU, memory, and logging configuration.
Domain Configuration
DomainName: A Route 53 record set for the domain, pointing to the ALB.
Outputs Section
Provides information about the created resources:

Cluster: The ECS cluster.
ApplicationLoadBalancerEndpoint: The DNS name of the ALB.
SecurityGroup: The security group ID for the ECS instances.
EFSID: The ID of the EFS file system.
AcceleratorDNS: The DNS name for the Global Accelerator.
