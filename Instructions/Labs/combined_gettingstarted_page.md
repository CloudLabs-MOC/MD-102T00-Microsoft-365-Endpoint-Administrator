# Getting Started with Your MD-102: Endpoint Administrator Workshop
 
Welcome to your MD-102: Endpoint Administrator workshop! We've prepared a seamless environment for you to explore and learn about deploying, configuring, protecting, managing, and monitoring devices and client applications in a Microsoft 365 environment. Let's begin by making the most of this experience:

> **!IMPORTANT**: Once you launch the track, you’ll have access to a virtual machine (VM) for **40 hours**. The displayed track duration of **4 days 8 hours (104 hours)** indicates the time frame during which you can use your VM. Please plan your lab sessions accordingly. If the VM uptime of **40 hours** is fully exhausted before completing the labs, access will be lost. To avoid this and for detailed instructions on VM usage and stopping/deallocating the VM, Refer to the **[Managing Your Virtual Machine](#managing-your-virtual-machine)** section for step-by-step instructions.

> If the full 40 hours of VM uptime is exhausted, the VM will no longer be accessible, and **the lab duration cannot be extended**.

## Overview

In these hands-on labs, you will develop the skills required to build, deploy, monitor, and troubleshoot AI-powered cloud solutions on Microsoft Azure. Working as an Azure Developer, you will implement Azure compute and containerization patterns, build serverless APIs with Azure Functions, and integrate services using event-driven and message-based architectures such as Azure Service Bus and Event Grid. The labs also cover Azure data services that support AI workloads, including Azure Cosmos DB for NoSQL, Azure Database for PostgreSQL with pgvector, and Azure Managed Redis for caching, streaming, and vector search. By completing these labs, you will gain the practical experience needed to connect services, orchestrate AI workflows, and build secure, scalable, and observable AI-driven applications on Azure.

## Objectives

By the end of these labs, you will be able to:

1. **Provision and configure Azure AI infrastructure:** Deploy and manage Azure AI resources, Azure Functions, Azure Container Apps, Azure Container Registry, and supporting Azure services required for AI-powered applications.

2. **Develop cloud-native AI applications:** Build serverless APIs, containerized applications, and backend services that integrate Azure AI capabilities using the Azure SDKs, REST APIs, and modern application development patterns.

3. **Implement event-driven and distributed architectures:** Design and integrate applications using Azure Service Bus, Azure Event Grid, and asynchronous messaging to enable scalable, loosely coupled AI workflows.

4. **Work with AI-ready data platforms:** Store, retrieve, and manage structured, unstructured, and vectorized data using Azure Cosmos DB for NoSQL, Azure Database for PostgreSQL with pgvector, Azure Managed Redis, and Azure Storage.

5. **Build intelligent search and retrieval solutions:** Implement vector search, semantic retrieval, and Retrieval-Augmented Generation (RAG) scenarios by combining Azure AI Search with vector-enabled databases and AI models.

6. **Deploy and manage containerized workloads:** Build, publish, deploy, and maintain container images using Azure Container Registry, Azure Container Apps, and Azure Container Registry Tasks.

7. **Secure AI applications and cloud resources:** Configure authentication, authorization, secrets management, managed identities, and network security to protect applications and Azure resources.

8. **Monitor, troubleshoot, and optimize applications:** Collect telemetry, diagnose failures, monitor application health, and improve the performance, scalability, and reliability of AI-powered cloud solutions using Azure monitoring and diagnostic tools.

9. **Integrate Azure services into end-to-end AI workflows:** Connect compute, messaging, storage, databases, and AI services to build automated, scalable, and production-ready intelligent applications.

10. **Apply cloud-native development best practices:** Build resilient, maintainable, and observable AI applications by following modern Azure development patterns, automation techniques, and operational best practices.

## Pre-requisites

- Experience with Azure development concepts.
- Proficiency in a programming language such as C# or Python is recommended.
- Familiarity with Azure compute, containerization, serverless development, event-driven architectures, data services, and REST APIs will help learners get the most from this course.

## Architecture

The lab architecture demonstrates how Azure's cloud-native services work together to build, deploy, integrate, and operate intelligent AI applications. Throughout these labs, you will provision compute resources, implement serverless and containerized workloads, connect applications using event-driven messaging, manage AI-ready data stores, and build secure, scalable, and observable AI-powered solutions.

1. **Azure AI Services and Azure OpenAI:** Provide the intelligence layer for AI-powered applications, enabling capabilities such as natural language processing, document understanding, embeddings, and generative AI experiences.

2. **Azure Compute Services:** Azure Functions, Azure Container Apps, and Azure Container Registry host and execute serverless APIs, containerized applications, and background processing workloads that power AI solutions.

3. **Azure Messaging and Integration Services:** Azure Service Bus and Azure Event Grid enable reliable, asynchronous communication between distributed services, allowing applications to respond to events and orchestrate AI workflows.

4. **Azure Data Services:** Azure Cosmos DB for NoSQL, Azure Database for PostgreSQL with pgvector, Azure Managed Redis, and Azure Storage provide persistent storage, vector search, caching, streaming, and document storage for AI-enabled applications.

5. **Azure Developer Tools:** Azure Portal, Azure CLI, Visual Studio Code, Azure SDKs, and REST APIs are used to provision infrastructure, deploy applications, manage cloud resources, monitor workloads, and troubleshoot AI solutions throughout the labs.

## Explanation of Components

1. **Azure AI Services & Azure OpenAI:** Provide prebuilt and generative AI capabilities that enable applications to understand, generate, and process text, images, documents, and other content using REST APIs and Azure SDKs.

2. **Azure Functions:** Executes event-driven, serverless code that processes requests, orchestrates AI workflows, and integrates Azure services without managing infrastructure.

3. **Azure Container Apps:** Hosts containerized AI applications and APIs, providing scalable, managed execution for microservices and background processing workloads.

4. **Azure Container Registry (ACR):** Stores and manages container images used by Azure Container Apps and other Azure compute services, supporting secure image versioning and deployment.

5. **Azure Service Bus:** Provides reliable message queues and publish/subscribe messaging that decouple application components and enable asynchronous communication between AI services.

6. **Azure Event Grid:** Delivers events from Azure resources and applications, allowing services to react automatically to changes and trigger downstream AI workflows.

7. **Azure Cosmos DB for NoSQL:** Stores application data, conversation history, metadata, and other structured information using a globally distributed NoSQL database.

8. **Azure Database for PostgreSQL with pgvector:** Stores relational data while enabling vector similarity search, supporting Retrieval-Augmented Generation (RAG) and semantic search scenarios.

9. **Azure Managed Redis:** Improves application performance through distributed caching, streaming, session management, and vector search capabilities.

10. **Azure Storage:** Provides secure storage for documents, images, datasets, application assets, and other files processed by AI applications.

11. **Azure SDKs & REST APIs:** Enable developers to integrate Azure services into applications, automate workflows, and interact programmatically with Azure resources.

12. **Azure Portal & Azure CLI:** Provide graphical and command-line tools for provisioning resources, deploying applications, monitoring services, and managing Azure infrastructure throughout the labs.

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and lab guide will be right at your fingertips within your web browser.
 
  ![Access Your VM and Lab Guide](../media/MD712.png)

### Virtual Machine & Lab Guide
 
Your virtual machine is your workhorse throughout the workshop. The lab guide is your roadmap to success.
 
## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment Details** tab.
 
  ![Explore Lab Resources](../media/envtab.png)
 
## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the Top right corner.
 
![Use the Split Window Feature](../media/splittab.png)
 
## Lab Progress

You can use the **Progress** tab to track your progress while working on the lab. A score will be provided after successful validation.

![Use the Split Window Feature](../media/progresstab.png)

## Managing Your Virtual Machine

1. Feel free to **Start, Restart, or Stop (2)** your virtual machine as needed from the **Resources (1)** tab. Your experience is in your hands!
 
    ![Manage Your Virtual Machine](../media/restab.png)

2. To Switch between the Virtual Machines, select the required VM from the dropdown.

   ![](../media/switch.png)

   > **Note :** If you’re unable to switch the VM from the dropdown menu, you can also access the VM directly from the desktop of your Host VM.

    ![](../media/1.png)

## Lab Guide Zoom In/Zoom Out
 
To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

   ![](../media/Zoomtab.png)

## Pasting Commands in the PowerShell/CloudShell Environment

Please make sure to use the **CTRL+SHIFT+V** or **CTRL+V** keys when pasting commands inside the PowerShell/CloudShell environment instead of right-clicking

## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels explicitly tailored for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.
 
Learner Support Contacts:
 
- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

- Click on **Next** from the lower right corner to move on to the next page.

  ![](../media/pgn.png)

Now you're all set to explore the powerful world of technology. Feel free to reach out if you have any questions along the way. Enjoy your workshop!
 
## Happy Learning !!
