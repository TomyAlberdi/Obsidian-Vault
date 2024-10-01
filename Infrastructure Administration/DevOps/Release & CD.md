Created: 2024-10-01 19:01
## Family Tree:
1. Computer
2. Infrastructure Administration
3. [[DevOps]]
-- -
The processes of **continuous delivery** and **continuous deployment** follow the same stages, but with one key difference.
- **Continuous delivery** focuses on automating the steps to ensure our software is ready to be deployed to production environments at any time. However, it **does not** automatically deploy the software to production!
- **Continuous deployment** takes it one step further. In this practice, **everything is automated**, even in production environments! The goal is to eliminate human intervention in any part of the workflow. This is the most significant difference compared to continuous delivery.
To achieve this, the **production pipeline** has a series of steps that must be executed in the correct order and successfully — and all **automatically**! If any of these steps do not complete as expected, the deployment process will not be carried out.