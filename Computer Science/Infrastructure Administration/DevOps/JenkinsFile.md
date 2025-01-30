Created: 2024-10-01 17:03
## Family Tree:
1. Computer
2. Infrastructure Administration
3. [[DevOps]]
-- -
A **JenkinsFile** is a file that contains the rules or steps to be executed within a pipeline. It can be written in either a **Declarative** or **Scripted** format. The JenkinsFile is stored in the repository alongside the rest of the project's code.
## Declarative JenkinsFile
The **Declarative** syntax is structured and easier to read. It consists of several blocks:
- **Pipeline Block**: The main block, which houses all the other blocks.
- **Stage Block**: Each **stage** represents a phase of the pipeline (e.g., build, test, deploy), and is used by plugins to visualize the status and progress of the pipeline.
- **Step Block**: Each **step** defines a specific task for Jenkins to execute at different points in the pipeline cycle.
### Example:
```jenkinsfile
pipeline {
  agent any // Specifies the agent where the pipeline will run
  stages {
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing...'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying...'
      }
    }
  }
}
```
In this example:
- **Agent any**: Jenkins will run the pipeline on any available agent.
- **Stages**: There are three stages—Build, Test, and Deploy—each performing a basic task like printing a message (`echo`).
## Scripted JenkinsFile
The **Scripted** syntax offers more control and flexibility compared to the declarative approach. However, it is more complex, written in a Groovy-like language, and has a steeper learning curve.
#### Characteristics:
- **Greater Power and Flexibility**: Allows for more advanced logic and control structures.
- **Complexity**: Due to its more granular approach, scripted pipelines can be more difficult to write and maintain.