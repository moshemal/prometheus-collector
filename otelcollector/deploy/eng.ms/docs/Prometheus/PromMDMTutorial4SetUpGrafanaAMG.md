> [!Note]
> Prometheus metrics in MDM is still in active development. It is only available for a very small set of customers to provide very early feedback - limited private preview. Geneva will open this up for broader preview, after we've had a chance to address feedback received in the current limited preview. If your team has not already been contacted for the limited preview, then you are not yet eligible for this preview. You can also join the [K8s Observability Updates](https://idwebelements/GroupManagement.aspx?Group=K8sObsUpdates&Operation=join) alias for updates on this feature, including when this will roll out more broadly.

# Setup Azure Grafana Service

Grafana is a popular open source tool that allows you to query, visualize, alert on and understand your metrics no matter where they are stored. You can install and manage Grafana yourself, or make use of a managed Grafana service. A managed Grafana service will allow you to focus only on creating your dashboards and visualizations, without the overhead involved in installing, maintaining, securing and scaling your data.  

## Azure Managed Workspace for Grafana

There are two versions of Azure managed Grafana at present - an early Dogfood service and the private preview of Azure Managed Workspace for Grafana:

* If you are using Grafana to query Prometheus metrics from MDM, we strongly recommend that you onboard the private preview directly (instead of Dogfood). If you are already on Dogfood, you will be asked to migrate to the private preview in the near future.
* If you are using Grafana to query classic (non-Prometheus) MDM metrics, you will start with the Dogfood and be asked to migrate to the preview at a later date.

### Prerequisites for Azure Managed Workspace for Grafana preview

To join the private preview, please send your Azure subscription ID to [this email](mailto:ad4g@microsoft.com) with a subject line *Request to join private preview*. We ask you to limit to one subscription due to the current capacity constraints.

### Prerequisites for Azure Managed Grafana Dogfood

If you have not done this already at the beginning of the tutorial, you will need to have performed these before you proceed with the tutorial.

* For this step, you will be using a preview version of Azure Grafana Service, and need access to a dogfood subscription. If you do not yet have one, please request one via [this email](mailto:ad4g@microsoft.com)
* Also to be able to set up data sources and dashboards, you will need to have 'Grafana Admin' access. To do this [join the Azure Dashboard for Grafana Dogfood (Admin) group](https://idweb/identitymanagement/aspx/groups/MyGroups.aspx?popupFromClipboard=%2Fidentitymanagement%2Faspx%2FGroups%2FEditGroup.aspx%3Fid%3Daa23b20a-f5ef-485d-94bd-468bbf2346fb) via IDWeb.

## Grafana and data sources

To connect Grafana with metrics in metrics store, you would use a [data source](https://grafana.com/docs/grafana/latest/datasources/), which will import data from a metrics store. Grafana has several built-in data sources (including one for Prometheus) and you can add to it by writing your own. We will use Grafana and Prometheus data source to visualize/query the metrics we collected in previous steps.

If you are using the Azure Managed Workspace for Grafana preview, you can find setup instructions at [our doc repo](https://github.com/microsoft/azure-grafana-preview-doc). You will need a Microsoft GitHub account to access the repo.

The rest of this tutorial applies to the Azure Managed Grafana Dogfood service. In either case, please also join the [Azure Grafana Service](https://teams.microsoft.com/l/team/19%3aU7k7xgekXyKeLAIS8igygU0-6vFHk9W243x16DOVPng1%40thread.tacv2/conversations?groupId=4e24cc02-a532-453a-bfeb-0089595e72e7&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47) team to get support, report issues and provide feedback.

## Create Grafana cluster

To use Azure Grafana for your team, you will create a Grafana cluster. This is done by adding it as a resource.  

* Go to the [Azure dogfood portal](https://aka.ms/ags/portal/df)  

![AMG](~/metrics/images/prometheus/AMGMain.png)  
  
* Create a Grafana cluster  

Click 'Create'  
![Create Cluster](~/metrics/images/prometheus/AMGCreateCluster.png)  
  
* Enter cluster information  

    - **Subscription** - Ensure this is set to the dogfood subscription you are part of  
    - **Resource group** - Create a new resource group for your team, or reuse one your team may have created already  
    - **Instance name** - Provide an instance name of your choosing for your cluster  
    - **Region** - Please select 'East US'  

![Create Cluster desc](~/metrics/images/prometheus/AMGCreateClusterFields.png)  
  
* Proceed to **Review + Create**
![Create Cluster desc](~/metrics/images/prometheus/AMGCreateClusterFields3.png)  
  
* Proceed with **Create**  
  
* View created Grafana cluster resource  

When deployment completes, you will see a **Go to resource** option to view the created Grafana resource. Click it.
![Grafana Resource](~/metrics/images/prometheus/AMGGoToGrafanResource.png)  
  
* Get cluster host name  
To access your newly created Grafana cluster, you need its host name. For this click the host name and you will be taken to Grafana website.  

![Grafana HostName](~/metrics/images/prometheus/AMGGrafanResourceHostName.png)  

> [!Note]
> The actual resource creation will take about 8 minutes. Even if you see resource creation marked as succeeded, the Grafana website may not be accessible for ~ 8 minutes.  
  
* Login to your Grafana instance  

Clicking the host name URL should take you to the Grafana portal. If you see 'Continue to external URL' option, click it.  
You may also see a login prompt. Azure Grafana Service makes this simple by allowing you to login with your Microsoft credentials.  

Click 'Sign in with Microsoft' to login  
![Login](~/metrics/images/prometheus/AMGLogin.png)

Upon successful login you will see the Grafana home page. Go to Manage dashboards to see some sample dashboards that are already set up for you.  
![Manage](~/metrics/images/prometheus/AMGGrafanaPostSignIn.png)

--------------------------------------

In this step you set up Azure Grafana Service.  

Next, you lets connect Grafana to access the Prometheus metrics in your Geneva Metrics (MDM) account. [Configure Prometheus data source](~/metrics/prometheus/PromMDMTutorial5AddPromDataSource.md)