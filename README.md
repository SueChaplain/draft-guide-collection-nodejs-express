

# Kabanero Collections

A Kabanero Collection defines a logical set of software components for developing applications that can be built and deployed to container platforms.

These components include the application stack for a specific programming language, plus container build and deployment artifacts such as Tekton pipelines. Multiple collections are available, including those for Java, Node, and Spring.

By using a Kabanero Collection, you benefit from industry best practices. Each collection uses components that are known to integrate and work well together, which allows you to develop, test, and deploy applications faster, without specialist knowledge in the underlying container technology.

If necessary, a collection can be customized to meet local requirements. For example, you might want to define specific maintenance levels of software components or expose a particular port for your application. Customizing a collection provides a mechanism for controlling the precise development and runtime environment for an application. In a large organization, customization ensures that applications are developed and tested with a level of consistency that promotes quality and helps guarantee a seamless implementation in your production environment.

You can select any number of Kabanero Collections to meet your needs, including those that support your migration from traditional applications to cloud-native applications with microservices.

## Using Kabanero Collections

As a developer in a large organisation, you typically don't have to deal with all the components of Kabanero. The Kabanero Foundation software might already be installed and configured by an operations team, which provides some of the underlying services that are required on top of an OKD or Red Hat OpenShift deployment. In addition, the Kabanero Collections available to you might have been chosen and customized in some way to meet local security policies. Your experience of using a Kabanero Collection will be similar to using Appsody out-of-the-box, as described in the [Appsody Documentation](https://appsody.dev/docs).

## Using the Node.js Kabanero Collections

There are 3 Kabanero Collections for Node.js; one that includes just the runtime environment (`nodejs`) and others that include the Express or LoopBack frameworks (`nodejs-express` or `nodejs-loopback`). The way in which you use these collections is similar. In this guide we will explore how to use the `nodejs-express` Kabanero Collection when using VS code as an IDE.

### Prerequisites

1) You must have Docker installed on your local system.

2) VS Code requires the Codewind extension from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.codewind). When you install the extension, a Codewind workspace is created for you and Docker images are downloaded to your Docker registry.

Note: Because Codewind includes Appsody code, you must remove any local installations of Appsody before installing the Codewind extension to avoid possible conflicts. Run `brew uninstall Appsody` and manually remove the `.Appsody` folder from your filesystem.

If you are using Eclipse Che instead of VS Code, install the Codewind extension from the [Eclipse Marketplace](https://marketplace.eclipse.org/content/codewind).

3) Codewind requires an Appsody extension, which you can obtain from the [appsodyExtension GitHub repo](https://github.com/kabanero-io/appsodyExtension). Follow the instructions for **Installing the Appsody Extension on Codewind** and **Adding the Appsody Templates** to your Codewind workspace.

To complete the installation, stop and restart Codewind by right-clicking on your **codewind** folder in your VS Code interface, and selecting **stop**. Right-click again and select **start**.

You are now ready to create your first project!

### Creating a project from a collection

Open your VS Code Explorer menu and find the **CODEWIND** folder. Click the '+' symbol on the Projects folder to create a new project.

A window is displayed with a list of available project types. Select the **Appsody template for Nodejs-express**. Choose a suitable name for your project and press **Enter** to save it.

<!--NOTE: In a large organisation, you might be given a specific location for choosing your development stack. These stacks might be customized to meet local requirements.-->

A new project is created, built, and started inside a container, which is linked to the VS Code workspace. Projects are created with a default set of files, which you can find in a project folder in your **CODEWIND-WORKSPACE**. Click on `app.js` to view the "Hello from Appsody" app.

To see the running app, right-click on the project in the **CODEWIND** folder and click **open**. Your browser will open to display "Hello from Appsody!" on a local port number.

Codewind watches for file changes and automatically updates your application. If you edit `app.js` to change the "Hello from Appsody!" string, you can refresh your browser to see the text update straight away.

You are now ready to develop your own app!

### Developing and testing your app

As you progress with developing your app in VS Code, you are likely to want to do some local testing. As well as checking whether your code runs cleanly you can also look at application metrics and performance monitoring.

#### Viewing application metrics

Right-click on the running project in the **CODEWIND** folder and select **Open Application Monitor** to open the  dashboard. Graphical information is displayed about CPU, Memory, and HTTP trafic.

#### Viewing performance monitoring

Right-click on the running project in the **CODEWIND** folder and select **Open Performance Dashboard**, which allows you to run load tests.

### Deploying your app on a local Kubernetes cluster



### Deploying your app to a production environment
