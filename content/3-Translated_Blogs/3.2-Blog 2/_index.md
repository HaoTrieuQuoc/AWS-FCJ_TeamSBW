---
title : "Blog 2"

weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---
## **Right-size Kubernetes with metrics-driven GitOps automation**  
Authors: Hari Charan Ayada and Ioannis Moustakis | Date: September 11, 2025 | In:  [Amazon Bedrock](https://aws.amazon.com/blogs/containers/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Elastic Kubernetes Service](https://aws.amazon.com/blogs/containers/category/compute/amazon-kubernetes-service/), [Technical How-to](https://aws.amazon.com/blogs/containers/category/post-types/technical-how-to/)

Efficient resource allocation in Kubernetes is essential to optimize application performance and control costs. In [Amazon Elastic Kubernetes Service (Amazon EKS)](https://aws.amazon.com/eks/), managing resource requests and limits manually can be difficult and error-prone. This post introduces an automated, GitOps-based approach to resource optimization using Amazon Web Services (AWS) such as [Amazon Managed Service for Prometheus](https://aws.amazon.com/prometheus/) and [Amazon Bedrock](https://aws.amazon.com/bedrock/). This approach is especially useful for users who prefer non-intrusive resource optimization.

**Understanding the challenges of resource management on Amazon EKS**

Understanding resource management in Kubernetes is critical for optimal cluster performance. When you deploy a pod, the Kubernetes scheduler evaluates resource requests to find a suitable node that can meet the specified CPU and memory requirements. These requests act as the minimum guaranteed resources for the pod, while limits act as upper boundaries to prevent any pod from monopolizing node resources.

### **Impact of inefficient resource management**

Over-provisioning and under-provisioning resources in Kubernetes can lead to increased costs and performance issues. Getting the balance right is essential for optimal resource utilization. In a shared environment, a pod that consumes too many resources can degrade the performance of other pods on the same node. Applications with fluctuating resource demands can be hard to manage. Without an adaptive resource allocation strategy, these workloads can suffer performance degradation or waste resources. Furthermore, manually tuning resource requests and limits for dynamic workloads can be time-consuming and prone to human error.

**Existing solutions for Kubernetes resource management**

[**The Vertical Pod Autoscaler (VPA)**](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler) or **[Goldilocks](https://github.com/FairwindsOps/goldilocks)** in recommendation mode, while useful, require installation in the cluster, which means additional tools to manage, additional resource consumption, and configuration per workload. Sometimes, teams do not have the flexibility to install custom tooling in the cluster due to strict regulatory or security requirements. Other tools, such as [Robusta KRR](https://github.com/robusta-dev/krr), can run as a CLI, but use strategies to calculate resource recommendations such as the 95th percentile, while still requiring custom implementation to integrate advanced machine learning (ML)-based strategies.

VPA and [Horizontal Pod Autoscaler (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/) can be used independently, but careful consideration is needed when using them together to avoid scaling conflicts. There are other tools such as [StormForge](https://stormforge.io/), which use an automated agent and allow direct editing of requests and limits in the cluster. Although these solutions integrate with GitOps tools, they break the principle of Git as the source of truth for configuration, which may be unacceptable in strictly controlled environments.

While [Helm](https://helm.sh/) and [Kustomize](https://github.com/kubernetes-sigs/kustomize) make manifest management more convenient, they create a major challenge for automated updates: identifying the correct template file or values file to edit when a resource recommendation is available. Resource usage metrics and recommendations often relate to the final Kubernetes objects (such as Deployments or StatefulSets), but the change must be applied to the source template or the relevant values files in the Git repository. This separation introduces complexity, because knowing the optimal CPU/memory for a specific Deployment is not enough.

### **How the proposed solution addresses the challenge**

This post proposes a non-intrusive solution that can optimize resources without modifying the cluster or disrupting existing autoscaling mechanisms, while using pull requests as a change-management mechanism. The solution runs outside the production EKS cluster and integrates multiple available options for advanced configuration strategies, such as forecasting algorithms. Our proposed pattern uses the native rendering logic in GitOps tools such as Argo CD. We incorporate a [manifest rendering](https://akuity.io/blog/the-rendered-manifests-pattern) step so the workflow can accurately map the recommended resource changes back to the source files in the Git repository. As a result, automation can precisely target the files to edit and create a pull request to update the templates. This ensures the changes integrate with the existing GitOps process, closing the gap between resource recommendations and template updates.

### **Solution overview**

This post introduces an architecture pattern for automatically optimizing Kubernetes resource requests and limits, as illustrated in the following figure, combining the following three key components:
![Image](/images/3.translated_blogs/image_1_blog2.png) 
<p align="center"><em>Figure 1: End-to-end solution flow triggered on a schedule to optimize Kubernetes resource utilization</em></p>

1. **Metrics-driven analysis**: Use Amazon Managed Service for Prometheus to collect and analyze historical resource usage patterns across your Amazon EKS workloads.

2. **GitOps-driven delivery**: Use [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) to maintain a declarative approach to resource management, ensuring all changes are version-controlled and auditable.

3. **Pattern-aware optimization**: Support multiple workload patterns through specialized [resource optimization strategies](https://github.com/aws-samples/K8sResourceResizer/blob/dev/K8sResourceResizer/README.md#resource-optimization-strategies):

* Time-series analysis for applications with business-hours patterns

* Trend-awareness to handle sudden spikes in resource demand

* Workload-aware optimization for the characteristics of each deployment

* Statistical ensembling across Quantile Regression, Moving Average, and Prophet for comprehensive pattern analysis

The solution runs on a recurring schedule, automatically creating pull requests with recommended values based on a recommendation engine with configurable options. This is combined with generative AI through Amazon Bedrock to explain the changes and generate pull request descriptions. Organizations can apply this pattern to continuously improve resource utilization while maintaining GitOps principles for collaboration, version control, and auditing.

**Workflow overview**

1. The workflow is triggered at a recurring interval as required via [GitHub Actions](https://github.com/features/actions). As the first step, we clone the repository containing the Kubernetes configuration.  
2. We retrieve historical resource usage data from Amazon Managed Service for Prometheus, which is connected to your production cluster, and compute recommended values for each deployment’s limits and requests based on configurable strategies.  
3. The workflow creates a temporary local Kubernetes cluster and deploys [Argo CD](https://argo-cd.readthedocs.io/en/stable/).  
4. Using the Argo CD CLI, the workflow renders the complete Kubernetes manifests based on multiple configuration values, overlay layers, and environment overrides. This enables the workflow to accurately map the proposed resource changes back to specific source files in the Git repository, allowing precise targeting of the correct files.  
5. Once updated values are available, we call Amazon Bedrock with the new values and the existing manifests and ask it to create a pull request with a description and explanation of the changes. To ensure the model produces the pull request content correctly, we provide in-context learning examples along with the prompt.  
6. The workflow creates a new branch and a pull request on the GitHub repository with the changes containing the new Kubernetes limits and request values, along with a related description.  
7. Finally, a developer must review the pull request and merge it so that a deployment is rolled out according to GitOps best practices.

**Key architectural elements**

The solution integrates multiple safeguards to ensure production stability. Resource recommendations are bounded by configurable minimum and maximum thresholds to prevent extreme adjustments. Furthermore, the recommendation engine does not interact directly with the production Kubernetes cluster and therefore avoids the need to install additional tools and increasing the cluster’s potential attack surface.

This architecture integrates seamlessly with established GitOps practices and existing CI/CD pipelines. Resource updates are handled through the same approval process as other infrastructure changes, maintaining consistency and control. The solution supports multiple infrastructure as code (IaC) formats such as raw Kubernetes manifests, Helm charts, and Kustomize overlays. It includes the ability to analyze and update resource definitions regardless of the templating mechanism used.

The solution uses the long-term metrics storage capabilities of Amazon Managed Service for Prometheus to maintain a rich history of resource usage patterns. This historical data informs the recommendation algorithms and supports compliance requirements for change documentation. The solution includes configurable retention policies for recommendations and related metrics data, ensuring alignment with organizational governance standards. The architecture promotes collaboration by clearly delineating responsibilities between platform teams and application teams. Platform teams can set global policies and guardrails, while application teams retain control over their specific workload configuration. The automated pull request process includes detailed context about recommendations, enhanced with explanations and descriptions powered by generative AI and Amazon Bedrock, enabling well-informed review decisions. Integration with notification systems ensures relevant stakeholders are aware of proposed changes and can participate in the review process.

**Walkthrough**

In this walkthrough, we provide detailed guidance on how to do the following:

1. Set up an environment capable of querying Amazon Managed Service for Prometheus to compute resource recommendations.

2. Integrate the resulting resource configuration updates into your GitOps workflow to automatically create pull requests, review, and deploy.

The walkthrough uses a sample application scenario to illustrate the process. It compares the resource configuration before and after and shows screenshots of the pull request and deployment status. Follow these steps to learn how to reproduce this solution in your own environment.

**Prerequisites**

Before you begin, make sure you have the following:

* An AWS account.

* An EKS cluster configured with a GitOps tool such as Argo CD.

* Access to Amazon Managed Service for Prometheus.

* A working CI/CD pipeline.

* Basic understanding of containers and Kubernetes concepts.

**Deploying GitOps-based automation for resource optimization**

The following sections walk you through deploying a GitOps-based automation process to optimize resources.

**GitOps principles**  
The GitOps model treats infrastructure and application definitions as version-controlled artifacts. Any changes to Kubernetes manifests are made via pull requests in a central Git repository, enabling clear audit trails, review workflows, and rollback when needed.

**Setting up the recommendation generator**  
You can integrate a recommendation generator with GitOps to automate resource optimization in a controlled, review-based workflow. The generator runs outside the cluster, references metrics to produce CPU and memory request/limit recommendations, and creates pull requests to update manifests in your Git repository. This setup operates outside the cluster and relies on existing metrics, thereby avoiding any impact on cluster operations or performance. A GitOps tool, such as Argo CD, detects and deploys these updates after they are approved and merged.

**Environment and metrics source**  
To deploy this solution, you must start with an EKS cluster. Next, verify that Amazon Managed Service for Prometheus is correctly configured to collect the required CPU and memory usage data from your cluster. You must set up a Git repository to store and version-control Kubernetes manifests, including all required Deployments and other configuration files. Finally, deploy a GitOps tool such as Argo CD to continuously monitor your repository for changes, ensuring that your cluster state always matches the desired configuration defined in the Git repository.

[This GitHub link](https://github.com/aws-samples/K8sResourceResizer.git) is an example of creating an EKS cluster and a Prometheus workspace to get started with Terraform.

**Local or external installation**  
As a first step, clone the resource optimizer repository:

git clone https://github.com/aws-samples/K8sResourceResizer.git

Set up your recommendation generator in an environment outside the cluster, such as a dedicated instance, a containerized solution, or integrated into your existing CI/CD pipeline runner. Once it’s set up, ensure the generator is configured correctly with the required credentials and endpoints to access and query historical metrics from Amazon Managed Service for Prometheus. With this configuration, run the tool to analyze current and historical usage data and generate resource optimization recommendations tailored to your workload requirements. In this guide, we set up the recommendation generator as part of a [GitHub Actions](https://github.com/features/actions) CI/CD pipeline.

**Automating the GitOps process**

To set up the workflow in GitHub Actions:  
1\. Build and push the recommendation generator Docker image from the [Dockerfile](https://github.com/aws-samples/K8sResourceResizer/blob/dev/K8sResourceResizer/Docker/Dockerfile) and the [source code](https://github.com/aws-samples/K8sResourceResizer/tree/dev/K8sResourceResizer/Src) of the repository you cloned to your own container image registry. You can find instructions in the [GitHub repository readme file](https://github.com/aws-samples/K8sResourceResizer/tree/dev/K8sResourceResizer), or you can use our example [GitHub Actions workflow to build and push to ECR](https://github.com/aws-samples/K8sResourceResizer/blob/dev/.github/workflows/build-and-push.yml). To set up connectivity to AWS, [follow this guidance](https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/) to configure an [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) role according to best practices.

2\. After you have the recommendation generator Docker image in your own container image registry, set up a GitHub Actions workflow on the repository where you store Kubernetes manifests or templates. This is an example of a [GitHub Actions Workflow](https://github.com/aws-samples/K8sResourceResizer/blob/dev/K8sResourceResizer/README.md#github-actions-setup-with-iam-roles-recommended-for-production) that triggers this flow on a configurable cron schedule, is parameterized with different configuration options for recommendations, and uses an IAM role for authentication. Visit the [Strategy Selection](https://github.com/aws-samples/K8sResourceResizer/blob/main/K8sResourceResizer/README.md#strategy-selection) section of the code repository to understand the different available strategies and how to choose one. To set it up, configure [IAM roles with GitHub Actions](https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/) and set these values as [GitHub secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions):

* AMP\_WORKSPACE\_ID: Amazon Managed Prometheus workspace ID  
* AWS\_REGION: AWS Region  
* GITHUB\_TOKEN: GitHub token for authentication

3\. [Trigger the GitHub Actions workflow manually](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/manually-running-a-workflow) and verify that you receive a pull request created in your Kubernetes manifests repository.

The following illustrations show what the generated pull request looks like.
![Image](/images/3.translated_blogs/image_2_blog2.png) 
<p align="center"><em>Figure 2: Pull request description generated by Amazon Bedrock</em></p>

![Image](/images/3.translated_blogs/image_3_blog2.png) 
<p align="center"><em>Figure 3: Changes in the pull request based on the recommendations</em></p>

**Cleanup**  
To avoid incurring costs, delete all resources you created while testing this solution:

1. Go to the [AWS Management Console](https://aws.amazon.com/console/), locate the [Amazon Elastic Container Registry (Amazon ECR)](https://aws.amazon.com/ecr/) repository, and delete the solution’s recommendation container image.

2. Follow the [cleanup section of the GitHub repository](https://github.com/aws-samples/K8sResourceResizer/blob/main/PreRequirements/EKS/README.md#cleanup) and run the following command from the Amazon [EKS directory](https://github.com/aws-samples/K8sResourceResizer/tree/main/PreRequirements/EKS):

terraform destroy

**Conclusion**  
This solution demonstrates a practical, non-intrusive approach to Kubernetes resource optimization, combining the power of metrics-driven decision-making with GitOps principles. Organizations can use Amazon Managed Service for Prometheus for historical data analysis, Amazon Bedrock for intelligent manifest updates, and GitOps workflows through Argo CD to automate the resource optimization process while maintaining control and oversight over changes.

While this solution provides immediate value for resource optimization, it also serves as a foundation for more advanced automation scenarios. Organizations can build on this framework to integrate additional metrics, custom optimization algorithms, or integrations with cost management tools. We encourage users to start with a small set of non-critical workloads to become familiar with the process, then gradually expand coverage across more of their Kubernetes infrastructure. Teams can follow the implementation guidance and best practices presented in this post to achieve more efficient resource utilization while maintaining application stability and reliability.

To get started, visit our [GitHub repository](https://github.com/aws-samples/K8sResourceResizer) and follow the setup instructions. We welcome feedback and contributions from the community to help further evolve this solution.

---

**Hari Charan Ayada** is a Senior Solutions Architect at Amazon Web Services in Copenhagen.

**Ioannis Moustakis** is a Senior Solutions Architect at Amazon Web Services in Brussels.
