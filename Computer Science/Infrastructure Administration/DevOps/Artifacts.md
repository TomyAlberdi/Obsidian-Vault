Created: 2024-10-01 17:39
## Family Tree:
1. Computer
2. Infrastructure Administration
3. [[DevOps]]
-- -
An **artifact** is an object or a set of objects produced during the build process. These artifacts can be used for further builds or as the final compiled output. Applications are often divided into individual components that are assembled into a complete product. This usually happens during the build phase, where smaller fragments of the application are created. This process is designed to make more efficient use of resources, reduce build times, and improve binary debugging. The type of artifact depends on the product being used to develop the application.
## Common Artifact types by product
- **Java**: `.jar`, `.ear`, `.war`, etc.
- **.Net**: `.dll`, `.exe`, etc.
- **Python**: `.py`, `.sdist`
Artifacts can also include files not tied to a specific programming product but necessary for functionality, such as **YAML**, **XML**, **TXT**, **MD**, **lib**, **so**, **bin**, etc.
## Artifact Management
An artifact repository product allows teams to perform the following operations:
- **Move** artifacts
- **Copy** artifacts
- **Delete** artifacts:
  These operations ensure consistency across repositories. When an artifact is moved, copied, or deleted, the system should automatically update related **metadata descriptors** like `maven-metadata.xml`, **RubyGems**, **Npm**, etc.
## Metadata
**Metadata** refers to "data about data." Each artifact contains metadata, which is crucial for code reuse. For example, metadata can tell us if an artifact has been modified, providing information such as:
- Who made the change?
- When and at what time was it done?
- What dependencies does it have?
This metadata plays a key role in collaboration, allowing developers to share code and use third-party components. However, managing various types of metadata can complicate collaboration if not handled with a clear strategy from the start.
## Storage
While **code** is typically stored in version control systems like GitHub, GitLab, or BitBucket, **artifacts**—especially binary files—are handled differently. Storing large, unreadable binary files in project repositories doesn’t make much sense.
This is where **binary repositories** become vital to the **continuous integration** process. These repositories allow you to store all artifacts in a centralized location, simplifying management. Common products in this space include:
- **Artifactory**
- **Nexus**
- **Harbor**
Cloud-based options include:
- **Azure Artifact**
- **Artifact Registry**
## Immutability
In the context of **DevOps**, immutability means that once we create an artifact—whether it's a container image or a compiled code package—it should not need to be modified. If changes are required, a new version of the object will be created.
**Why is it useful for an object or artifact to be immutable?**
Because when we copy it— for example, from a development environment to production— we already know how it will behave. Not only must the artifact be immutable to work well in all environments, but the infrastructure must also be immutable.
### Immutability in Docker:
In this document, we will demonstrate the principle of immutability applied to containers.
To execute this example, we will need a Dockerized application to run locally. We'll use three files:
1. **`index.js`**, which will be the NodeJS application we will modify to create multiple versions:
```js
'use strict';

const express = require('express');
// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
```
2. **`package.json`**, which lists the dependencies and describes our application:
```json
{
  "name": "my_nodejs_app",
  "version": "1.0.0",
  "description": "Node.js in Docker",
  "author": "email@example.com",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.16.1"
  }
}
```
3. **Dockerfile**, which defines the container with the minimal requirements to run our application:
```dockerfile
FROM node:14

# Create app directory
WORKDIR /usr/src/app

# Install dependencies
COPY package*.json ./

RUN npm install

# Copy application source
COPY . .

# Expose port and run the application
EXPOSE 8080
CMD [ "node", "index.js" ]
```
#### Compiling a Dockerfile:
When we compile an application using Docker, we can do this as many times as necessary to publish changes to the application. However, if we always use the standard command:
```sh
docker build . -t node-app
```
This will generate an image of our application, tagging it with "latest."
Once the image is generated, we can run our application on port 8090 of our machine with:
```sh
docker run -p 8090:8080 -d node-app
```
### Best Practices:
To follow best practices, we apply the **immutability principle**, ensuring that each Docker image is unique.
Notice that if we generate a new image of the same program, the previous one is not deleted, though it loses its name and tag, but its ID can still be recovered. This is because Docker itself is immutable.
To take advantage of this platform, every time we make a change to our application, we should tag it with a version that represents the new state. Here's how:
- **V1**: This is our version with "Hello World."
- **V2**: The new version shows "Hello Again!"
We compile and tag version **V1**:
```sh
docker build . -t node-app:V1
```
We do the same for version **V2**:
```sh
docker build . -t node-app:V2
```
We can even run both versions in parallel, one on port 8090 and the second on port 8091, using the following commands:
```sh
docker run -p 8090:8080 -d node-app:V1
docker run -p 8091:8080 -d node-app:V2
```
We can verify this by accessing each URL in the browser at the same time.