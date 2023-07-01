# Ansible Playbook: Rolling Update for Auto Scaling Group

This Ansible playbook is designed to perform a rolling update on an Auto Scaling Group (ASG) of EC2 instances. The update involves deploying a website using a launch template for the ASG and Ansible to manage the configuration. After the initial deployment, subsequent updates to the website files can be made, and this playbook will perform the updates on each EC2 instance in a rolling fashion without terminating any servers.

## Prerequisites

Before running this playbook, ensure that you have the following prerequisites:

1. Ansible installed on the control machine.
2. AWS credentials with the necessary permissions to manage Auto Scaling Groups and EC2 instances.
3. SSH keypair (e.g., `aws.pem`) to authenticate with the EC2 instances.

## ASG Creation and Website Hosting

Before using this playbook, you need to set up the following:

1. **Create a Launch Template:** Create a launch template with the desired configuration, including the desired Amazon Machine Image (AMI), instance type, security groups, etc. This template will be used to launch instances within the ASG.

2. **Create an Auto Scaling Group:** Create an Auto Scaling Group using the launch template created in the previous step. Configure the scaling policy and desired capacity according to your requirements. This ASG will ensure the desired number of EC2 instances are running.

3. **Host Website Files:** Host your website files (HTML, CSS, JS, etc.) on a version control system like GitHub. This playbook assumes the website files are hosted on GitHub, but you can modify it to use any other source.

## Playbook Structure

The playbook consists of two plays:

1. **Creating Dynamic Inventory:** This play gathers information about EC2 instances within the Auto Scaling Group and creates a dynamic inventory for further deployment.

2. **Rolling Update Deployment:** This play runs on the EC2 instances and handles the deployment and configuration updates for the website.

## Usage

1. Clone the repository to your local machine:

```bash
git clone https://github.com/your-username/rolling-update-ansible
cd rolling-update-ansible
```

2. Update the necessary variables in the playbook according to your setup. You may need to modify the `vars` section in the playbook to specify your ASG details, GitHub repository URL, etc.

3. Run the playbook:

```bash
ansible-playbook rolling_update.yml
```

This will start the rolling update process, updating the website on each EC2 instance without causing any downtime.

Please ensure you have thoroughly tested your website and the rolling update process in a safe environment before running it in production.
