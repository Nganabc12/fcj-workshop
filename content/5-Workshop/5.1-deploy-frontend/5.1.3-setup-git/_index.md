---
title: "Setup Git Repository"
weight: 3
chapter: false
pre: " <b> 5.1.3 </b> "
---

# Setup Git Repository

In this step, we will set up the frontend source code for the Pet Resort & Care System and manage it on GitHub.

## 1. Prepare the Source Code on GitHub

Our project uses GitHub for version control. You can access the official repository directly here:

- **Repository Link**: [https://github.com/wuys-fan/web-dog-cat.git](https://github.com/wuys-fan/web-dog-cat.git)

If you want to create your own copy to practice the deployment process, follow these steps:

1. Log in to your GitHub account.
2. Go to the Repository link provided above.
3. Click the **Fork** button (top right corner) to create a copy in your personal account.
4. Ensure the **Visibility** of your new repository is set to your preference (**Public** or **Private**).

![GitHub Repository Structure](/images/1-Worklog/github_repository.png)

## 2. Clone the code to your Local Machine

Open your Terminal (or Git Bash/Command Prompt) on your computer and run the following command to download the code:

```bash
git clone [https://github.com/wuys-fan/web-dog-cat.git](https://github.com/wuys-fan/web-dog-cat.git)
cd web-dog-cat/frontend
```

Install the required dependencies for ReactJS:

```bash
npm install
```

---

## Next Steps

Continue with [Deploy Frontend to S3 & CloudFront](../5.1.4-deploy-frontend/) to host the application UI on AWS.