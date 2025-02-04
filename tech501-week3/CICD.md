- CI (Continuous Integration)
CI is the practice of frequently integrating code changes into a shared repository, where automated builds and tests run to detect issues early.

- Benefits:

- Early bug detection
- Faster feedback for developers
- Improves code quality
- Reduces integration problems
- Encourages collaboration



- CD (Continuous Delivery)
CD extends CI by automatically preparing code for deployment, ensuring it can be released at any time.

- Benefits:

- Reduces manual work in deployments
- Ensures stable releases
- Faster time-to-market
- Increases reliability through automation
- Difference Between CD and CDE

- CD (Continuous Delivery/Continuous Deployment): Automates code testing and deployment.
- CDE (Cloud Development Environment): A cloud-based workspace where developers write, test, and deploy code.


- Jenkins
Jenkins is an open-source automation server used to build, test, and deploy applications.

- Why Use Jenkins?
- Benefits:

- Automates build and deployment
- Scalable with plugins
- Supports CI/CD pipelines
- Works with multiple languages and tools


- Disadvantages:

- Requires maintenance
- Can be complex to configure
- Performance issues with large workloads


- Stages of Jenkins Pipeline
- Source: Fetches code from version control (GitHub, GitLab)
- Build: Compiles and packages the application
- Test: Runs unit and integration tests
- Deploy: Deploys to staging or production
- Monitor: Checks system health and logs


- Alternatives to Jenkins
- GitHub Actions
- GitLab CI/CD
- CircleCI
- Travis CI
- Azure DevOps
- ArgoCD (for Kubernetes)


- Why Build a Pipeline? 
- Business Value
- Reduces manual errors
- Ensures faster, reliable releases
- Improves developer productivity
- Increases deployment frequency
- Enhances software quality
- CI/CD Diagram


Heres a general diagram of CI/CD:

1 Developer pushes code →
2 CI Server (Jenkins, GitHub Actions, etc.) →
3 Build & Test →
4 Artifact Storage (S3, Nexus, Docker Hub, etc.) →
5 Deployment (Kubernetes, AWS, etc.) →
6 Monitoring & Feedback (Prometheus, ELK, etc.)

SDLC Workflow
Plan: Define requirements, scope
Design: Create architecture, UI/UX, tech stack
Develop:Write, test, and review code
Deploy: Release software and monitor