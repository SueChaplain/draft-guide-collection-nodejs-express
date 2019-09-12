
**>>>>>>>> WHAT IS A KABANERO COLLECTION**

# Kabanero Collections

A Kabanero Collection defines a logical set of software components for developing applications that can be built and deployed to container platforms.

These components include the application stack for a specific programming language, plus container build and deployment artifacts such as Tekton pipelines. Multiple collections are available, including those for Java, Node, and Spring.

By using a Kabanero Collection, you benefit from industry best practices. Each collection uses components that are known to integrate and work well together, which allows you to develop, test, and deploy applications faster, without specialist knowledge in the underlying container technology.

If necessary, a collection can be customized to meet local requirements. For example, you might want to define specific maintenance levels of software components or expose a particular port for your application. Customizing a collection provides a mechanism for controlling the precise development and runtime environment for an application. In a large organization, customization ensures that applications are developed and tested with a level of consistency that promotes quality and helps guarantee a seamless implementation in your production environment.

You can select any number of Kabanero Collections to meet your needs, including those that support your migration from traditional applications to cloud-native applications with microservices.

## Using Kabanero Collections

As a developer in a large organisation, you typically don't have to deal with all the components of Kabanero. The Kabanero Foundation software might already be installed and configured by an operations team, which provides some of the underlying services that are required on top of an OKD or Red Hat OpenShift deployment. In addition, the Kabanero Collections available to you might have been chosen and customized in some way to meet local security policies.

You can use collections directly from a terminal window by installing the Appsody CLI, or you can use collections within an IDE by installing Codewind. Supported IDEs are VS Code or Eclipse.

## Using the Node.js Kabanero Collections

There are 3 Kabanero Collections for Node.js; one that includes just the runtime environment (`nodejs`) and others that include the Express or LoopBack frameworks (`nodejs-express` or `nodejs-loopback`). The way in which you use these collections is similar. In this guide we will explore how to use the `nodejs-express` Kabanero Collection.

## What you will learn

In this guide you will learn how to create, run, update, deploy and deliver a simple cloud native application using the `nodejs-express` Kabanero Collection in your VS Code IDE.

## Prerequisites

1. You must have [Docker](https://docs.docker.com/get-started/) installed.
2. You must have access to a Kubernetes cluster. If you are using Docker for Desktop, you can enable Kubernetes from the menu by selecting Preferences -> Kubernetes -> Enable Kubernetes.
3. You must install the VS Code Codewind extension from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.codewind), which creates a **CODEWIND** workspace and downloads Docker images to your Docker registry.
4. (Optional) If you have an enterprise-specific Kabanero Collection Hub, you need the URL to your index file.

*Note:* Because Codewind includes Appsody code, you must remove any local installations of Appsody before installing the Codewind extension to avoid possible conflicts. Run `brew uninstall Appsody` and manually remove the `.Appsody` folder from your filesystem.

You are now ready to create your first project!

## Getting started

By default, Codewind is configured to use the public Kabanero Collection hub. If you have been given an enterprise-specific Kabanero
Collection Hub URL, configure your installation by following these steps:


**>>>>>>>>>>>>>>> NOTE: Need to add a step for setting the URL to the correct collection for the developer (Champ provides)**
**>>>>>>>>>>>>>>> At this point in time you cannot configure the repo in Codewind for VS Code**
<placeholder for steps ... equivalent to appsody repo list to see what's there / appsody repo add URL / appsody repo list for verification / appsody repo set-default NAME>

VS Code is now configured to use the Kabanero Collection Hub for your organisation.

The next step is to create a project folder for your application code. Open your VS Code Explorer menu and find the **CODEWIND** folder. To create a new project, click the '+' symbol on the Projects folder.

A list of available project types is shown. Select the **Appsody template for Nodejs-express**. Choose a suitable name for your project and press **Enter** to save it.

A new project is created, built, and started inside a container, which is linked to the VS Code workspace.

## Understanding the project layout

Projects are created with a default set of files, which you can find in a project folder in your **CODEWIND-WORKSPACE**.

![Diagram shows the VS Code project view](https://github.com/kabanero-io/draft-guide-collection-nodejs/raw/master/images/codewind-workspace.png)


Click on `app.js` to view the code for the "Hello from Appsody" app.

```
const app = require('express')()

app.get('/', (req, res) => {
  res.send("Hello from Appsody!");
});

module.exports.app = app;
```

To see the running app, right-click on the project in the **CODEWIND** folder and click **Open App**.

![Diagram shows the menu list for a project, with the Open App option highlighted](https://github.com/kabanero-io/draft-guide-collection-nodejs/raw/master/images/openapp.png)

Your browser opens to display "Hello from Appsody!" on a local port number.

![Diagram of a browser window, which displays the string "Hello from Appsody!"](https://github.com/kabanero-io/draft-guide-collection-nodejs/raw/master/images/nodejsexpress-project.png)

## Updating the application

Codewind watches for file changes and automatically updates your application.

Edit `app.js` to change the "Hello from Appsody!" string and then refresh your browser to see the text update straight away.

## Stopping the application

You can find information about the running app by opening the Project Overview. Right-click on the project in the **CODEWIND** folder and click **Open Project Overview**.

![Diagram shows the menu list for a project, with the Open Project option highlighted](https://github.com/kabanero-io/draft-guide-collection-nodejs/raw/master/images/openproject.png)

VS Code displays information about the status of the app, similar to the following screenshot:

![Diagram shows the Project Overview pane, which provides information about the status of the app](https://github.com/kabanero-io/draft-guide-collection-nodejs/raw/master/images/projectoverview.png)

To stop the application, click the **Disable project** button.

You are now ready to develop your own app!

At some stage in development, you are likely to want to do some local testing. As well as checking whether your code runs cleanly, Codewind provides application metrics, performance monitoring, and debugging capabilities. For more information about developing applications with Codewind for VS Code, see the [Codewind documentation](https://www.eclipse.org/codewind/mdt-vsc-getting-started.html).


## Deploying to Kubernetes

<input needed>

## Deploying to KNative

<input needed>

## Delivering your app to your Enterprise production environment

When you've finished developing and testing your app, you are ready to deliver it to your enterprise Kabanero pipelines. This step involves pushing the project to a pre-configured git repository (public or enterprise). Your operations team should have configured the necessary hooks on the repository to trigger the pipelines that build and deploy your project into the production environment.
