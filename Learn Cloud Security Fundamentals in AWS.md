<img width="1536" height="672" alt="cloud-security-cover" src="https://github.com/user-attachments/assets/4daa98a0-9770-4e58-90e1-cfd529e87429" />



Security is a vital part of every system and infrastructure. The word "security" comes from the Latin securitas, which is composed of se- (meaning “without”) and cura (meaning “care” or “worry”). Originally, it meant "without worry." Over time, it has come to signify being safe or protected.

Security is a vital part of every system and infrastructure. The word "security" comes from the Latin securitas, which is composed of se- (meaning “without”) and cura (meaning “care” or “worry”). Originally, it meant "without worry." Over time, it has come to signify being safe or protected.

Today, when we discuss security, we usually refer to protection from harm, danger, or threats, whether in our homes, online, while using online banking, or even across an entire country. Security is important in everything we do.

Cloud providers, such as AWS, are no exception. Their infrastructure must be safeguarded to ensure users’ peace of mind. But on platforms like AWS, security is a shared responsibility. This means that both the provider and the user play a role in maintaining security.

Amazon Web Services (AWS) is one of the most popular cloud service providers worldwide. With great power and flexibility comes the responsibility to secure your cloud infrastructure, data, and applications.

In this guide, we’ll explore the fundamental aspects of cloud security on AWS, making it easy to understand for those new to cloud computing.

## What is Cloud Security?

Cloud security is the set of rules, tools, and practices used to protect your data, apps, and services stored online (in the "cloud"). It helps prevent data loss, hacking, and misuse of information.

Think of cloud security like locking the doors of your house. You wouldn’t leave your doors open for anyone to enter. And in the same way, your cloud account must be secured so that your data remains safe.

If your cloud services aren't secure, hackers could steal your data or cause major damage. Whether you're a business or just someone using cloud apps, keeping your information safe is essential.

## Why is Cloud Security Important?

Cloud security matters because it ensures that only the right people have access to your information. It protects your data from being lost, stolen, or misused. With good security in place, your applications can run safely without being exposed to attacks.

It also helps you keep your personal or business data private. When your cloud environment is well-protected, the risk of data breaches and financial loss is greatly reduced.

Now that you understand why cloud security is important, let’s look at how AWS helps you stay secure and what your own role is in keeping things safe.

## Key Cloud Security Concepts

In AWS, cloud security is the responsibility of both AWS and the customer. This model is called the Shared Responsibility Model.

Before learning how AWS divides security duties, you need to understand that AWS protects its infrastructure, but you must protect your own account.

When you create a new AWS account, you start with what is called the **root user**. The root user has full control, but it’s risky to use it for daily work. You should only use it to create another user, called an IAM (Identity and Access Management) user.

**Here is what you should do:**

- Use the root user once to create an IAM user.

- Do not use the root account for everyday work. Use IAM users instead.

- The principle of least privilege should be followed—that is, a user should be given only the access they need.

- Protect the root user by turning on a feature called MFA, or multi-factor authentication.

## What is MFA?

MFA adds another layer of security when you sign in. It combines something you know, like your password, with something you have, such as a phone or security device. Even if someone gets your password, they cannot log in without your MFA code.

**You can enable MFA in several ways:**

- Using a virtual MFA app like Google Authenticator or Authy

- Using a physical security key such as a YubiKey

- Using a hardware device from Gemalto

- For AWS GovCloud users, using an MFA device from SurePassID

Always enable MFA for both your root and IAM users. It’s one of the simplest and most effective ways to protect your AWS account.

So now that you know these fundamentals, we can talk about the shared responsibility model.

## Understanding the AWS Shared Responsibility Model
The AWS Shared Responsibility Model divides responsibilities between AWS and the customer.

### 1. AWS’s Responsibility (Security of the Cloud)
AWS is responsible for protecting the infrastructure that runs the services offered in the AWS Cloud. This includes physical security, hardware, software, networking, and facilities.

### 2. Customer’s Responsibility (Security in the Cloud)
The customer is responsible for securing the data, user accounts, applications, and configurations they store in the cloud.


![AWS shared responsibility model](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mj3usbsj508qy2ndexev.png)

Image source: [AWS shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model/)

For example, AWS is responsible for securing its data centres and servers. But customers also have a role to play by properly configuring their accounts and resources.

Let’s take two popular AWS services, RDS (Relational Database Service) and S3 (Simple Storage Service), as examples.

### RDS (Relational Database Service)

**AWS responsibilities:**

- Automates database patching

- Audits and maintains the underlying instance and storage disks

- Applies operating system patches automatically

**Customer responsibilities (you):**

- Manage in-database users, roles, and permissions

- Choose whether your database is public or private

- Review and control inbound rules, ports, and IP addresses in the database’s security group

- Configure database encryption settings

### S3 (Simple Storage Service)

**AWS responsibilities:**

- Ensures encryption options are available for your data

- Guarantees virtually unlimited storage capacity

- Prevents AWS employees and the public from accessing your data

- Keeps each customer’s data separated from others

**Customer responsibilities (you):**

- Define your S3 bucket policies according to your security standards

- Review bucket configuration settings

- Create and manage IAM users and roles with the right permissions

Now you understand who’s responsible for what.

## Conclusion
Security has always been about peace of mind. Whether it’s your home, your phone, or your cloud account, you want to know your data is safe.

AWS gives you a strong foundation by securing the cloud itself. But your part matters too, things like enabling MFA, using strong passwords, and managing who can access what. These simple habits go a long way in keeping your data protected.

Cloud security isn’t a one-time setup; it’s an ongoing practice. When both AWS and its users stay alert, the cloud becomes a place you can trust to store, build, and grow with confidence.

Now that you understand how security works in AWS, you’re ready to dive deeper and start exploring the services that keep it all running smoothly.

For a deeper and clearer explanation, you can read the full guide here:  [Learn Cloud Security Fundamentals in AWS](https://www.freecodecamp.org/news/learn-cloud-security-fundamentals-in-aws-a-guide-for-beginners/)

## Other Resources

- [How to Deploy a Kubernetes App on AWS EKS](https://www.freecodecamp.org/news/how-to-deploy-a-kubernetes-app-on-aws-eks/)

- [The Best AWS Services to Deploy Front-End Applications in 2025](https://www.freecodecamp.org/news/best-aws-services-for-frontend-deployment/)

- [What is Backend as a Service (BaaS)? A Beginner's Guide](https://www.freecodecamp.org/news/backend-as-a-service-beginners-guide/)

- [The Hidden Challenges of Building with AWS](https://dev.to/ijay/the-hidden-challenges-of-building-with-aws-8mg)

If you found this article helpful, feel free to share it. And if you prefer learning through videos, I also explain cloud topics in simple terms on my [YouTube channel](https://www.youtube.com/@cloudinreallife).

Stay updated with my projects by following me on [Twitter](https://twitter.com/ijaydimples), [LinkedIn](https://www.linkedin.com/m/in/ijeoma-igboagu/), and [GitHub](https://github.com/ijayhub).

Thank you for reading!




