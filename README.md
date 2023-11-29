#Reflective Analysis

Pipeline

The pipeline strategy, commonly known as CI/CD, is used to manage software development
through stages of build, test, and deploy the code. The primary goal of automating each stage of
the process is to reduce manual errors and ensure consistency until the software is released. To
accomplish this, different tools are employed based on the different stages of the pipeline,
performing tasks such as code compilation, analysis, unit testing with security, and creation of
binaries. Containerization of environments is also a vital component of the pipeline, with code
packages created in a container and deployed to the cloud. The core ideology of the CI/CD
pipeline is DevOps, which brings together both the Developer and Operations teams to work in
tandem for deploying software. The speed at which the code is deployed in a competitive
environment is a defining aspect of the CI/CD pipeline.


Phases in Pipeline

Code Repository Phase
The CI/CD pipeline tasks are triggered by updates to the repository. These updates can come
from automatic schedulers, user workflows, or repository updates, which notify the CI/CD to
execute the configured pipeline tasks.

GITHUB REPOSITORY:
The references for the Github repositories of Terraform EC2 Jenkins Creation [1] and WordCount
Flask APP [2] are included. The Terraform EC2 repository contains the JenkinsFile that is executed
once the build is started in the build phase of Jenkins.
The WordCount Flask APP repository contains the Dockerfile that is executed in the EC2 instance
for the creation Flask APP instance server that runs a Web Application.

CHALLENGES
I had trouble pushing the code to the repository that I created. It kept showing an authentication
failed message. Luckily, I found a solution to this problem. I created an access key in the GitHub
repository, which I used as a password to authenticate the push to the corresponding
repositories. The access key specifies the necessary access points and the number of days it will
be valid.

Build Phase
During the Build Phase, the source code is linked with its corresponding dependencies in order to
create a runnable instance that can be delivered to end customers. Unlike some other
programming languages, Python does not require compilation during this process. Additionally,
this phase can also involve building a Docker container that will be deployed in a Docker
environment. It's important to note that any configuration issues during this phase can result in
failures, which require immediate attention.

JENKINS BUILD PHASE
In Jenkins, two pipelines were created - one for Terraform EC2 Creation and another for building,
testing, and deploying the Flask web app to the created EC2 instance as a Docker image. The
Terraform EC2 Creation pipeline contains the necessary files for creating a VPC with an IGW
added to the routetable with the corresponding subnet. In this subnet, an EC2 Amazon Linux
instance is created and launched with the key. The Security Group of the EC2 instance gives
access for HTTP and TCP requests. After the EC2 instance is launched, the instance is logged in
using the ssh connection to install Docker. Here, the Flask App Docker image is created and
hosted.

The Web App files are scripted in Python. It contains a Flask app that runs the word counter,
paragraph counter, and number of characters. It also has a Dockerfile that is used to create a
Docker Flask app image in the EC2 instance. Initially, the Flask Web app is tested on the local
machine with the virtual environment. In this phase, the Web App files are checked out from the 
GitHub Code repo and created as a tar file with the required files.

CHALLENGES
I had a similar issue with the terraform command. It was not recognized and I had trouble running
it. However, I found a solution to this problem by configuring the full path where the command is
stored. To get the location of the command, I used "which terraform" and this solved the problem.
When I was creating a default VPC, it asked me to create subnets which caused me some issues.
I had trouble creating the default subnets, so I decided to create a new VPC with the
corresponding subnets. This solved my issue and I was able to proceed with the task at hand.


Test Phase

It's crucial to run critical automated tests to ensure that the code works correctly as intended.
This is the stage where any bugs are identified and prevented from reaching the end customers.
It's the responsibility of every developer to write corresponding test cases, which demonstrates
the behavior pattern approach to development. The test case runtime varies depending on the
size and capacity of the project, and it might take hours to execute, depending on the length of
the code files tested. However, this can be tackled by executing test cases in multiple phases.
Test suites are designed and executed in parallel to decrease the execution time. Identifying the
overlooked code errors by developers is crucial in this phase to maintain the code base.

JENKINS TEST PHASE

The unit test cases are written to test the html code and app.py files. The pytest and codecov tool
is used to execute the test cases and display the required report in html format. The CodeCov for
this Web Application is 82%.

CHALLENGES

I faced challenges in executing the code cov command to generate the html report. After some
analysis, i was able to get the reports.


Deploy Phase
After creating a runnable instance with all the necessary test cases, it's time to proceed with the
deployment to the production phase. Different production environments, such as staging and
production phases, are available to deploy the working instance. Once all the changes are
approved, the code is automatically deployed from the main branch to the production phase.

JENKINS DEPLOY PHASE

During the deploy phase, the web app tar file that was created is transferred into the EC2 instance
using scp and pem file with the public IP address. The files are then extracted, and a Docker
image is created. The necessary web app is then hosted using Docker commands. Additionally,
the Github repositories are checked for any vulnerabilities using Snyk.

CHALLENGES

Having trouble in copying the build folder of the tar file to the EC2 instance even with the pem file.
However, I found a solution by disabling stricthostkeychecking. Now I am able to successfully
copy to the EC2 instance from Jenkins.

Benefits

Jenkins is an excellent tool with a supportive community to address any issue we encounter. It is
a free and easy-to-install tool that offers a wide range of plugins tailored to meet specific
requirements. The fact that it is written in Java makes it even more appealing. Its test phase is
incredibly helpful in identifying bugs and addressing them promptly, enabling developers to save
costs before deploying code to the production phase.

Drawbacks

Most of the Jenkins plugins are developed by third-party sources, which can pose security risks.
Additionally, some settings in Jenkins Continuous Integration may experience occasional
disruptions, potentially impacting the automation of various phases.


DevOps Principles in Jenkins

Jenkins is a popular CI server that is well-known for its ability to orchestrate and automate the
integration of code changes coming from multiple developers. Its reliability and efficiency make it
a go-to choice for many developers.

With Jenkins at the center, teams can streamline their deployment processes and automate them
effortlessly. Its user-friendly interface and robust automation capabilities make it possible to
achieve seamless deployment, ensuring that the software is delivered to the end-users with
minimal effort and maximum efficiency.

Jenkins is a powerful tool that allows us to create a customized DevOps toolchain with ease. Its
plugin ecosystem is rich and tailored to meet the specific needs of the organization, ensuring that
our DevOps process is both efficient and effective.

Jenkins is a powerful tool for distributing workloads across multiple machines, resulting in faster
build, test, and deploy the processes. Its ability to automate these processes and manage them
across different environments makes it a popular choice for software development teams in the
DevOps process.

References
1. https://github.com/neeharicamadanu/terraformEc2
2. https://github.com/neeharicamadanu/CloudDevOps
3. Jesse Suen; Todd Ekenstam; Alex Matyushentsev; Billy Yuen, GitOps and Kubernetes:
Continuous Deployment with Argo CD, Jenkins X, and Flux , Manning, 2021.
4. Mohamed Labouardy, Pipeline as Code: Continuous Delivery with Jenkins, Kubernetes, and
Terraform , Manning, 2021.
5. S. Mysari and V. Bejgam, "Continuous Integration and Continuous Deployment Pipeline
Automation Using Jenkins Ansible," 2020 International Conference on Emerging Trends in
Information Technology and Engineering (ic-ETITE), Vellore, India, 2020, pp. 1-4, doi: 10.1109/
ic-ETITE47903.2020.239.
