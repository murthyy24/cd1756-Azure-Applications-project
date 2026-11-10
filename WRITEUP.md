# Write-up Template

### Analyze, choose, and justify the appropriate resource option for deploying the app.

*For **both** a VM or App Service solution for the CMS app:*
- *Analyze costs, scalability, availability, and workflow*
- *Choose the appropriate solution (VM or App Service) for deploying the app*
- *Justify your choice*

### Assess app changes that would change your decision.

*Detail how the app and any other needs would have to change for you to change your decision in the last section.* 


# Azure Applications Project Writeup

## Azure VM vs Azure App Service

### Cost
For a web application like this Article CMS, Azure App Service is simpler and more cost-effective to manage than running a full Virtual Machine.

With a VM, I would be responsible for the operating system, security updates, Python installation, web server configuration, and other infrastructure tasks. With App Service, Azure manages most of that for me, allowing me to focus more on the application.

### Scalability
Azure App Service also makes scaling easier. The application can be scaled up by moving to a larger App Service Plan or scaled out by adding more instances.

Doing the same with Virtual Machines would require additional VMs, load balancing, and more infrastructure configuration.

### Availability
App Service provides a managed hosting platform and offers availability features depending on the App Service Plan selected.

With Virtual Machines, achieving similar availability would normally require multiple VMs, load balancing, and additional configuration such as Availability Zones or Availability Sets.

### Deployment and Maintenance
App Service provides a straightforward way to deploy a Python web application without having to configure and maintain an entire server.

For this project, I deployed the Flask application to a Linux Azure App Service using Python 3.11 and Gunicorn.

A VM would give me more control, but it would also mean managing the operating system, Python runtime, security patches, firewall rules, and application processes myself.

## My Deployment Choice

I chose Azure App Service for the Article CMS because the application is a standard Flask web application and does not need direct access to or control over the underlying operating system.

The final solution uses:

- Azure App Service to host the Flask application
- Azure SQL Database to store users and article information
- Azure Blob Storage to store uploaded article images
- Microsoft Entra ID and MSAL for Microsoft authentication
- Azure App Service Log Stream to capture successful and failed login activity

I tested the deployed application using both the built-in username/password login and Microsoft authentication. I also verified that articles are stored in Azure SQL Database and uploaded images are stored and displayed from Azure Blob Storage.

Overall, App Service was the better fit because it provided everything this application needed without the additional administration required by a Virtual Machine.

## When I Would Choose a Virtual Machine

I would consider using an Azure Virtual Machine if the application had future requirements such as:

- Full control over the operating system
- Installation of software or system-level dependencies that are not supported by App Service
- Custom networking or server configuration
- Long-running background processes outside the normal web application model
- Specialized software that requires direct access to the host machine

The current Article CMS does not need those capabilities, so Azure App Service provides a simpler and more practical solution.