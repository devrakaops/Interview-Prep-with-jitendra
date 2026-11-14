### 1. What is CI/CD, and why is it used in software development?

**Answer:** CI/CD stands for **Continuous Integration** and **Continuous Delivery / Continuous Deployment**. It is a set of automated practices that help developers build, test, and release code changes faster, more frequently, and with fewer bugs compared to manual deployments.

---

### 2. What is Continuous Integration (CI)?

**Answer:** Continuous Integration is the practice where developers frequently merge their code changes into a shared repository (like GitHub). Every time code is pushed, an automated server (like Jenkins) automatically builds the code and runs unit tests to catch errors early.

---

### 3. What is the difference between Continuous Delivery and Continuous Deployment?

**Answer:**

* **Continuous Delivery:** Code is automatically built, tested, and prepared for release, but a human must click a button (manual approval) to deploy it to production.
* **Continuous Deployment:** Every change that passes all automated tests is deployed straight to production automatically without any human intervention.

---

### 4. Walk through a simple end-to-end CI/CD workflow from a `git push` to deployment.

**Answer:**

1. A developer writes code and runs `git push` to GitHub.
2. GitHub sends a notification (Webhook) to Jenkins.
3. Jenkins pulls the latest code from GitHub.
4. Jenkins compiles/builds the application (e.g., creating a `.jar` file or Docker image).
5. Jenkins runs automated tests. If tests fail, the pipeline stops and alerts the developer.
6. If tests pass, Jenkins deploys the application to a staging or production server.

---

### 5. What is Jenkins, and why is it so popular?

**Answer:** Jenkins is a free, open-source automation server written in Java. It is popular because it supports thousands of plugins, integrates easily with almost every developer tool (Git, Docker, Maven, AWS), and allows teams to automate their entire build, test, and deployment pipelines.

---

### 6. What is a Webhook in GitHub, and how does it trigger a Jenkins build?

**Answer:** A Webhook is an automated HTTP POST message sent from GitHub to Jenkins whenever a specific event occurs (such as a `git push` or a Pull Request). When GitHub detects a push, it instantly pings the Jenkins URL, telling Jenkins to start running the pipeline immediately without waiting or polling.

---

### 7. What is the difference between Poll SCM and a Webhook in Jenkins?

**Answer:**

* **Poll SCM:** Jenkins repeatedly asks GitHub on a schedule (e.g., every 5 minutes), *"Are there any new changes?"* This wastes server resources.
* **Webhook:** GitHub notifies Jenkins the exact second a change happens. Webhooks are faster and much more efficient.

---

### 8. What is a Jenkins Pipeline?

**Answer:** A Jenkins Pipeline is a suite of plugins and a structured workflow that defines the entire CI/CD process (Build, Test, Deploy) as code. Instead of clicking through the Jenkins UI manually, you write the pipeline steps in a text file.

---

### 9. What is a `Jenkinsfile`, and where is it stored?

**Answer:** A `Jenkinsfile` is a plain text file that contains the code/instructions for a Jenkins Pipeline. It is stored directly inside the root directory of your project's Git repository so it can be version-controlled alongside your application code.

---

### 10. Which programming language is used to write a `Jenkinsfile`?

**Answer:** A `Jenkinsfile` is written in **Groovy** (specifically, a Groovy-based Domain Specific Language or DSL).

---

### 11. What is the difference between Declarative Pipeline and Scripted Pipeline in Jenkins?

**Answer:**

* **Declarative Pipeline:** The modern, recommended syntax. It is simpler, easier to read, and uses a strict structure starting with a `pipeline { ... }` block.
* **Scripted Pipeline:** The older syntax written in pure Groovy starting with a `node { ... }` block. It offers more flexibility for complex logic but is harder to write and maintain.

---

### 12. What is inside a basic `Jenkinsfile`? (Give a simple example structure)

**Answer:** A basic Declarative `Jenkinsfile` contains `pipeline`, `agent`, `stages`, and `steps`:

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running automated tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
            }
        }
    }
}

```

---

### 13. What are `stages` and `steps` in a Jenkins Pipeline?

**Answer:**

* **`stages`:** High-level phases of your pipeline that divide the workflow into logical sections (e.g., `Checkout`, `Build`, `Test`, `Deploy`). They appear as columns in the Jenkins UI.
* **`steps`:** The actual individual commands executed inside each stage (e.g., `sh 'mvn clean package'` or `echo 'Hello'`).

---

### 14. What are the common stages in a standard CI/CD pipeline?

**Answer:**

1. **Checkout / Clone:** Pulling the source code from GitHub.
2. **Build:** Compiling the code and creating an executable artifact.
3. **Unit Test:** Running automated tests on the code.
4. **Code Quality / Security Scan:** Checking for bugs or vulnerabilities (e.g., using SonarQube).
5. **Package / Dockerize:** Creating a container image or archive file.
6. **Deploy:** Pushing the application to a staging or production server.

---

### 15. How do you build a Java project inside Jenkins?

**Answer:** Java projects are usually built using build tools like **Maven** or **Gradle**. Inside a Jenkins pipeline step, you run the build command:

* For Maven: `sh 'mvn clean package'` (this compiles the code, runs tests, and creates a `.jar` or `.war` file).
* For Gradle: `sh './gradlew build'`

---

### 16. Which tools are commonly used for Building, Testing, and Deploying in a CI/CD pipeline?

**Answer:**

* **Build Tools:** Maven, Gradle (for Java), npm/Yarn (for Node.js), pip (for Python), Docker (for containers).
* **Testing Tools:** JUnit, TestNG (for Java), PyTest (for Python), Jest (for JavaScript), Selenium (for UI testing).
* **Deployment Tools / Platforms:** Docker, Kubernetes, AWS (EC2, S3, ECS), Ansible, or SSH/SCP scripts to copy files to a Linux server.

---

### 17. How does deployment actually happen in a simple Jenkins setup?

**Answer:** In a basic setup, Jenkins uses **SSH** (via plugins like *Publish Over SSH* or `sshagent`) to connect to a remote server, copies the built artifact (like `app.jar` or a Docker image) to that server, and runs a command to restart the application service.

---

### 18. What is the Jenkins Controller (Master) and Agent (Node) architecture?

**Answer:**

* **Jenkins Controller (formerly Master):** The main server that hosts the Jenkins UI, schedules jobs, stores configurations, and monitors agents. It should not run heavy builds itself.
* **Jenkins Agent (formerly Slave/Node):** A separate machine (Linux VM, Windows machine, or Docker container) connected to the Controller that actually executes the build, test, and deployment jobs.

---

### 19. Why do we use Jenkins Agents instead of running everything on the Controller?

**Answer:**

1. **Performance:** Heavy builds won't crash or slow down the main Jenkins dashboard.
2. **Security:** Untrusted build scripts stay isolated from Jenkins' core configuration files.
3. **Environment Variety:** You can attach different agents for different needs (e.g., a Linux agent for Docker builds, a Windows agent for `.NET` builds).

---

### 20. What does `agent any` vs `agent none` mean in a `Jenkinsfile`?

**Answer:**

* `agent any` tells Jenkins to run the pipeline on **any available** agent or executor.
* `agent none` tells Jenkins not to assign a global agent for the entire pipeline; instead, each individual `stage` will specify its own agent.

---

### 21. How do you add a new Agent (Node) to Jenkins?

**Answer:**

1. Go to **Manage Jenkins -> Nodes -> New Node**.
2. Give the node a name and select **Permanent Agent**.
3. Configure the **Remote root directory** (a folder on the agent machine where Jenkins will work, like `/home/ubuntu/jenkins`).
4. Choose a launch method (usually **Launch agents via SSH** using the agent's IP address and SSH credentials).
5. Save the settings and verify the agent comes online.

---

### 22. Where is the Jenkins Home Directory (`JENKINS_HOME`) located, and what does it store?

**Answer:** On a standard Linux installation, `JENKINS_HOME` is located at **`/var/lib/jenkins`**. It is the most important folder in Jenkins because it stores all job configurations, build logs, installed plugins, user credentials, and system settings.

---

### 23. How do you install and manage Plugins in Jenkins?

**Answer:**

1. Click **Manage Jenkins** on the left menu.
2. Select **Plugins** (or *Manage Plugins*).
3. Go to the **Available plugins** tab, search for the plugin you need (e.g., *Git*, *Pipeline*, *Docker Pipeline*), check its box, and click **Install**.
4. You can also upload a `.hpi` plugin file manually under the **Advanced settings** tab.

---

### 24. Where do you configure global tools like Java (JDK), Git, and Maven in Jenkins?

**Answer:** You go to **Manage Jenkins -> Tools** (formerly *Global Tool Configuration*). Here you can specify the installation paths (like `JAVA_HOME` or `MAVEN_HOME`) or tell Jenkins to install them automatically.

---

### 25. Where do you set Environment Variables and Secrets (like passwords or API keys) in Jenkins?

**Answer:**

* **Global Environment Variables:** Set under **Manage Jenkins -> System -> Global properties -> Environment variables**.
* **Pipeline-level Variables:** Defined inside a `Jenkinsfile` using an `environment { ... }` block.
* **Passwords & API Keys:** Stored securely under **Manage Jenkins -> Credentials** (never hardcoded as plain text in a `Jenkinsfile`).

---

### 26. What is a `post` block in a Jenkins Pipeline?

**Answer:** A `post` block defines actions that run **after** all the `stages` finish, depending on the pipeline's result. Common conditions include `always` (e.g., cleaning up workspace files), `success` (e.g., sending a green Slack message), and `failure` (e.g., sending an alert email to developers).

---

### 27. What is an Artifact in CI/CD?

**Answer:** An artifact is the final compiled output file produced by a build pipeline—such as a `.jar`, `.war`, `.zip`, or a Docker image. Artifacts are saved so they can be tested and deployed to servers without rebuilding the source code again.

---

### 28. What is the difference between a Freestyle Project and a Pipeline Project in Jenkins?

**Answer:**

* **Freestyle Project:** Configured purely through the web UI using forms and dropdowns. Good for simple, one-off tasks, but hard to maintain or version-control for complex workflows.
* **Pipeline Project:** Configured using code (`Jenkinsfile`). Ideal for full CI/CD workflows because it is stored in Git, supports complex multi-stage logic, and survives server restarts.

---

### 29. What happens if a step fails in the middle of a Jenkins Pipeline?

**Answer:** By default, Jenkins immediately stops executing the remaining stages, marks the build status as **FAILED** (red), jumps straight to any `post { failure { ... } }` block to send notifications, and prevents broken code from ever reaching deployment.

---

### 30. What is a Multibranch Pipeline in Jenkins?

**Answer:** A Multibranch Pipeline automatically discovers all branches and Pull Requests in your GitHub repository. If a branch contains a `Jenkinsfile`, Jenkins automatically creates a separate pipeline job for that branch and builds it whenever new commits are pushed.

---
