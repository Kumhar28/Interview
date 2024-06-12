# Jenkins Interview Questions

#### Continuous Integration: 
- A software development process where the changes made to software are integrated into the main code as and when a patch is ready so that the software will be always ready to be - built, tested, deployed, monitored - continuously.

#### Continuous Delivery: 
This is a Software Development Process where the continuously integrated (CI) changes will be tested & deployed continuously into a specific environment, generally through a manual release process, after all the quality checks are successful

#### Continuous Deployment: 
A Software Development practice where the continuously integrated (CI) changes are deployed automatically into the target environment after all the quality checks are successful

#### What are the ways to trigger a Jenkins Job/Pipeline?
- There are many ways we can trigger a job in Jenkins. Some of the common ways are as below -

- Trigger an API (POST) request to the target job URL with the required data.
- Trigger it manually from the Jenkins web application.
- Trigger it using Jenkins CLI from the master/slave nodes.
- Time-based Scheduled Triggers like a cron job.
- Event-based Triggers like SCM Actions (Git Commit, Pull Requests), WebHooks, etc.
- Upstream/Downstream triggers by other Jenkins jobs.

#### What are the credential types supported by Jenkins?
- In Jenkins, credentials are a set of information used for authentication with internal/external services to accomplish an action. Jenkins credentials are provisioned & managed by a built-in plugin called - Credentials Binding - plugin. Jenkins can handle different credentials as follows -

- Secret text - A token such as an API token, JSON token, etc.
- Username and password - Basic Authentication can be stored as a credential as well.
- Secret file - A secret file used to authenticate some secure data services & security handshakes.
- SSH Username with a private key - An SSH public/private key pair for Machine to Machine authentication.
- Certificate - a PKCS#12 certificate file and an optional password.
- Docker Host Certificate Authentication credentials.

- And as we can guess, this can be extended to several other extensible credential types like - AWS credential, Azure secrets, etc. using commonly available plugins.

#### What are the Scopes of Jenkins Credentials?
- Jenkins credentials can be of one of the two scopes - Global & System

- Global - the credential will be usable across all the jobs configured in the Jenkins instance (i.e. for all jobs). This is more suited for user Jobs (i.e. for the freestyle, pipeline, or other jobs) to authenticate itself with target services/infrastructures to accomplish the purpose of the job)

- System - This is a special scope that will allow the Jenkins itself (i.e. the core Jenkins functionalities & some installed plugins) to authenticate itself to external services/infrastructures to perform some defined tasks. E.g. sending emails, etc.

#### What is a Jenkins Shared Library and how it is useful?
- As an organization starts using more and more pipeline jobs, there is a chance for more and more code being duplicated in every pipeline job, since a part of the build/automation processes will be the same for most of the jobs. In such a situation, every other new upcoming job should also duplicate the same piece of code. To avoid duplications, the Jenkins project brought in the concept of Shared Libraries, to code - DRY - Don't Repeat Yourself.

- Shared libraries are a set of code that can be common for more than one pipeline job and can be maintained separately. Such libraries improve the maintenance, modularity & readability of the pipeline code. And it also speeds up the automation for new jobs.


#### What happens when a Jenkins agent is offline and what is the best practice in that situation?
- When a job is tied to a specific agent on a specific node, the job can only be run on that agent and no other agents can fulfill the job request. If the target node is offline or all the agents on that particular node are busy building other jobs, then the triggered job has to wait until the node comes online or an agent from that node becomes available to execute the triggered build request.

- As a result, a triggered job may sometimes wait indefinitely without knowing that the target node is offline. So, it is always the best practice to tie the jobs to a group of nodes & agents, referred to with a 'Label'. Once a job is tied to a Label, instead of a specific node/agent, any of the nodes/agents falling under the label can fulfill a build request, when a job is triggered. This way we can reduce the overall turn-around time of the builds.

- Even then if a job is waiting for more time for the nodes/agents, then it is time to consider adding more nodes/agents.

#### What is the Blue Ocean?
- Blue Ocean is the redefined user experience for Jenkins. Designed from the ground up for Jenkins Pipeline, it is still compatible with freestyle jobs, Blue Ocean reduces clutter and increases clarity. Blue Ocean’s main features include -

- Sophisticated visualizations of continuous delivery (CD) Pipelines, allowing for fast and intuitive comprehension of your Pipeline’s status.
- Pipeline editor - makes the creation of Pipelines approachable by guiding the user through an intuitive and visual process to create a Pipeline.
- Personalization to suit the role-based needs of each member of the team.
- Pinpoint precision when intervention is needed and/or issues arise. Blue Ocean shows where in the pipeline attention is needed, facilitating exception handling and increasing productivity.
- Native integration for branch and pull requests, enables maximum developer productivity when collaborating on code with others in GitHub, Bitbucket, etc.
Conventional UI - Job Details Page


#### Differences Between Jenkins Scripted and Declarative Pipeline

##### Scripted Pipeline

- Scripted Pipeline is the original pipeline syntax for Jenkins, and it is based on Groovy scripting language. 
- In Scripted Pipeline, the entire workflow is defined in a single file called a Jenkinsfile. 
- The Jenkinsfile is written in Groovy and is executed by the Jenkins Pipeline plugin. 
- Scripted Pipeline provides a lot of flexibility and control over the workflow, but it can be more complex and verbose than Declarative Pipeline.


```
node {
    stage('Build') {
        // Build the application
        sh 'mvn clean install'
    }
    stage('Test') {
        // Run the tests
        sh 'mvn test'
    }
    stage('Deploy') {
        // Deploy the application
        sh 'deploy.sh'
    }
}
```
##### Declarative Pipeline

- Declarative Pipeline is a more recent addition to Jenkins and provides a more structured and simpler syntax for defining pipelines. 
- Declarative Pipeline is based on the Groovy programming language, but it uses a Groovy-based DSL (Domain-Specific Language) for pipeline configuration.
- The main benefit of Declarative Pipeline is its readability and ease of use, as it is designed to be more intuitive and less verbose than Scripted Pipeline.
- we define a pipeline using the `pipeline block`, and we specify the `agent` to run the pipeline on any available node. 
- We then define three `stages` using the stages block, and we use the `steps block` to define the individual steps for each stage.

```
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Build the application
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                // Run the tests
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy the application
                sh 'deploy.sh'
            }
        }
    }
}
```


#### Example:

```
pipeline {
    agent any
    tools {
	    maven "MAVEN3"
	    jdk "OracleJDK8"
	}

    environment {
        registryCredential = 'ecr:us-east-2:awscreds'
        appRegistry = "951401132355.dkr.ecr.us-east-2.amazonaws.com/vprofileappimg"
        vprofileRegistry = "https://951401132355.dkr.ecr.us-east-2.amazonaws.com"
        cluster = "vprofile"
        service = "vprofileappsvc"
    }
  stages {
    stage('Fetch code'){
      steps {
        git branch: 'docker', url: 'https://github.com/devopshydclub/vprofile-project.git'
      }
    }


    stage('Test'){
      steps {
        sh 'mvn test'
      }
      input{
        massage "Are you sure?"
        ok "Yes"
      }
    }

    stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

        stage('build && SonarQube analysis') {
            environment {
             scannerHome = tool 'sonar4.7'
          }
            steps {
                withSonarQubeEnv('sonar') {
                 sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                }
            }
        }

        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }

    stage('Build App Image') {
       steps {
       
         script {
                dockerImage = docker.build( appRegistry + ":$BUILD_NUMBER", "./Docker-files/app/multistage/")
             }

     }
    
    }

    stage('Upload App Image') {
          steps{
            script {
              docker.withRegistry( vprofileRegistry, registryCredential ) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
            }
          }
     }
     
     stage('Deploy to ecs') {
          steps {
        withAWS(credentials: 'awscreds', region: 'us-east-2') {
          sh 'aws ecs update-service --cluster ${cluster} --service ${service} --force-new-deployment'
        }
      }
     }

  }
}

```
- input parameter will give you appoval msg to yes or no
- parallel:- This block is used to run steps in parallel
- dir:- 
#### Build Steps

https://phoenixnap.com/kb/jenkins-build-freestyle-project

https://www.jenkins.io/doc/book/pipeline/syntax/

### Jenkins
- Jenkins is an open-source Continuous Integration server written in Java for orchestrating a chain of actions to achieve the Continuous Integration process in an automated fashion.

### Jenkins Job
- Provde job name
Types:
1. Free style Project:
  - 
2. Pipeline:
  - 

## Reusable pipelines

How do I design a rollback pipeline using Jenkins

Why are we using shared libraries in Jenkins and its benefits?

### Optimizing an Effective CI/CD Pipeline
- Choose the right tools
- Streamline your workflow and remove unnecessary steps
- Monitor and measure your pipeline
- Automate and standardize your pipeline
- Implement feedback and continuous improvement
- Parallelize builds and tests by splitting your build and test processes into multiple parallel jobs that can run concurrently. This can significantly reduce the overall pipeline execution time.

### Jenkins - Shared Library

- A Jenkins Shared Library is a powerful feature that allows you to share and reuse code across multiple Jenkins pipelines or jobs. 
- It is essentially a collection of reusable Groovy scripts and resources that can be accessed and utilized in various Jenkinsfile scripts.
- Global Pipeline Libraries in system configuration in manage jenkins.
- Example creating 100 pipelines for diffternt microservices
- It is a common reusable code
- Create a liabrary in jenkins and refer it to or call it in Jenkins file
- Example: To inport liabrary `@Liabray("my-shared-Library") _` put at the start of pipeline
- Change in one place and it will reflected to all Pipelines
- Easy to fix issues.

```groovy
def call() {
  sh 'echo Hi from Sandeep, from shared liabrary'
}

```

