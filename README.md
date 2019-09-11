
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

**>>>>>>>>>>>>>> MATT's USING COLLECTIONS WITH THE APPSODY CLI**

### Using a collection in a terminal window with the Appsody CLI

When you use the Appsody CLI from a terminal window, your experience of using a Kabanero Collection will be similar to using Appsody out-of-the-box, as described in the [Appsody Documentation](https://appsody.dev/docs).

- **>>>>>>>>>>>>>> MATT's What you will learn**
- **>>>>>>>>>>>>>> MATT's What you will learn**

You will learn how to create, run, update, deploy and deliver a simple cloud native microservice application using the Kabanero java-microprofile collection and Appsody.

- **>>>>>>>>>>>>>> MATT's Prerequisites**

To complete the guide you will need to:

1) Install Docker

*TO DO - Do we need to include this step*

2) Install the Appsody CLI

*TO DO - Do we link to instructions or have to add them*

3) Have access to the Kabanero index file you will be using:

*TO DO - This could be a direct link to out github release or may be enterprise specific*

- **>>>>>>>>>>>>>> MATT's Getting Started**

First you need to add your Kabanero index to the Appsody CLI, in the example below we use the public index for Kabanero 0.1.2:

First check the existing repositories

`appsody repo list`

You should see output similar to

```
appsody repo list
NAME          URL
*appsodyhub    https://github.com/appsody/stacks/releases/latest/download/incubator-index.yaml
```

Now add the Kabanero index

```
appsody repo add kabanero https://github.com/kabanero-io/collections/releases/download/v0.1.2/kabanero-index.yaml
```

and check it has been added

```
appsody repo list
NAME          URL
*appsodyhub    https://github.com/appsody/stacks/releases/latest/download/incubator-index.yaml
kabanero      https://github.com/kabanero-io/collections/releases/download/v0.1.2/kabanero-index.yaml
```

Set the Kabanero index to be the default

`appsody appsody repo set-default kabanero`

Check it updated

```
appsody repo list
NAME          URL
appsodyhub    https://github.com/appsody/stacks/releases/latest/download/incubator-index.yaml
*kabanero      https://github.com/kabanero-io/collections/releases/download/v0.1.2/kabanero-index.yaml
```

You Appsody CLI is now configured to use the Kabanero collections.

Next you need to initialise you project, first create a directory to contain it

```
mkdir -p ~/projects/simple-microprofile
cd ~/projects/simple-microprofile
```

you can now initialise the project using the Appsody CLI

`appsody init java-microprofile`

the output from the command will vary depending on whether you have an installation of Java and Maven on your system. The example below is from a system with neither installed.

```
[InitScript] Unable to find any JVMs matching version "(null)".
[InitScript] No Java runtime present, try --request to install.
[InitScript] Unable to find a $JAVA_HOME at "/usr", continuing with system-provided Java...
[InitScript] No Java runtime present, requesting install.
[Warning] The stack init script failed: exit status 1
[Warning] Your local IDE may not build properly, but the Appsody container should still work.
[Warning] To try again, resolve the issue then run appsody init with no arguments.
Your project is now initialised.
```

- **>>>>>>>>>>>>>> MATT's Understanding the project layout**

*TO DO - Lift from Graham Charter workshop*

- **>>>>>>>>>>>>>> MATT's Running the Appsody development environment**

Start the Appsody development environment in preparation for developing the microservice:

`appsody run`

the Appsody CLI will launch a local docker image containing a Open Liberty server which will host the microservice. After a period of time you will see messages similar to the following

```
[Container] [INFO] [AUDIT   ] CWWKF0011I: The defaultServer server is ready to run a smarter planet. The defaultServer server started in 20.235 seconds.
this indicates that the server is started and you are ready to begin development.
```
- **>>>>>>>>>>>>>> MATT's Updating the application**

First navigate to the JAX-RS application endpoint to confirm that there are no JAX-RS resources available. Open the following link in your browser:

http://localhost:9080/starter

You should see an HTTP 500 error with the following message stating that there are no provider or resource classes associated with the application:

```
Error 500: javax.servlet.ServletException: At least one provider or resource class should be specified for application class "dev.appsody.starter.StarterApplication
```

Within your project folder navigate to the `src/main/java/dev/appsody/starter` folder. Within the folder create a file named `StarterResource.java`. Open the file in your editor and update to read

```
package dev.appsody.starter;
import javax.ws.rs.ApplicationPath;
import javax.ws.rs.core.Application;
@ApplicationPath("/starter")
public class StarterApplication extends Application {
 System.out.println("Hello from simple-microprofile");
}
```

when saved you should see the source being compiled and the application updated

```
[Container] [INFO] [AUDIT   ] CWWKT0017I: Web application removed (default_host): http://85862d8696be:9080/
[Container] [INFO] [AUDIT   ] CWWKZ0009I: The application starter-app has stopped successfully.
[Container] [INFO] [AUDIT   ] CWWKT0016I: Web application available (default_host): http://85862d8696be:9080/
[Container] [INFO] [AUDIT   ] CWWKZ0003I: The application starter-app updated in 0.988 seconds.
```

Now if you browse http://localhost:9080/starter you will no longer see the HTTP 500 error. The resource we just added is actually available at a location under `starter`. Browse the following URL to see the resource response:
http://localhost:9080/starter/resource


which should show

```
StarterResource response
```

Try changing the message in `StarterResource.java` saving and refreshing the page. You'll see it only takes a few seconds for the change to take effect.

When you're done, use `Ctrl-C` to end the appsody run.

- **>>>>>>>>>>>>>> MATT's Stopping the application**
- **>>>>>>>>>>>>>> MATT's Deploying to K8s**
- **>>>>>>>>>>>>>> MATT's Deploying to KNative**
- **>>>>>>>>>>>>>> MATT's Deliver to enterprise pipelines**

**>>>>>>>>>>>>>> End of MATT's list for using the Appsody CLI**



**>>>>>>>>>>>>>> SUE's USING COLLECTIONS WITH YOUR IDE VIA CODEWIND**

### Using a collection in your IDE

**>>>>>>>>>>>>>> SUE's WHAT YOU WILL LEARN**

 In this section we will explore how to use the `nodejs-express` Kabanero Collection when using VS code as an IDE, which requires the Eclipse Codewind extension.

**>>>>>>>>>>>>>> SUE's PREREQS**

#### Prerequisites

1) You must have Docker installed on your local system.

2) VS Code requires the Codewind extension from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.codewind). When you install the extension, a Codewind workspace is created for you and Docker images are downloaded to your Docker registry.

**>>>>>>> Was the case last week - check**
Note: Because Codewind includes Appsody code, you must remove any local installations of Appsody before installing the Codewind extension to avoid possible conflicts. Run `brew uninstall Appsody` and manually remove the `.Appsody` folder from your filesystem.

If you are using Eclipse instead of VS Code, install the Codewind extension from the [Eclipse Marketplace](https://marketplace.eclipse.org/content/codewind).

To complete the installation, stop and restart Codewind by right-clicking on your **codewind** folder in your VS Code interface, and selecting **stop**. Right-click again and select **start**.

You are now ready to create your first project!

**>>>>>>>>>>>>>> SUE's GETTING STARTED**

#### Creating a project from a collection

**>>>>>>>>>>>>>>> NOTE: Need to add a step for setting the URL to the correct collection for the developer (Champ provides)**

Open your VS Code Explorer menu and find the **CODEWIND** folder. Click the '+' symbol on the Projects folder to create a new project.

A window is displayed with a list of available project types. Select the **Appsody template for Nodejs-express**. Choose a suitable name for your project and press **Enter** to save it.

<!--NOTE: In a large organisation, you might be given a specific location for choosing your development stack. These stacks might be customized to meet local requirements.-->

**>>>>>>>>>>>>>> SUE's UNDERSTANDING THE PROJECT LAYOUT - add more here**

A new project is created, built, and started inside a container, which is linked to the VS Code workspace. Projects are created with a default set of files, which you can find in a project folder in your **CODEWIND-WORKSPACE**. Click on `app.js` to view the code for the "Hello from Appsody" app.

![VS Code project view](https://github.com/kabanero-io/draft-guide-collection-nodejs/raw/master/images/nodejsexpress-project.png)

```
const app = require('express')()

app.get('/', (req, res) => {
  res.send("Hello from Appsody!");
});

module.exports.app = app;
```

**>>>>>>>>>>>>>> SUE's RUNNING THE APPLICATION**

To see the running app, right-click on the project in the **CODEWIND** folder and click **Open App**. Your browser will open to display "Hello from Appsody!" on a local port number.

**>>>>>>>>>>>>>> SUE's UPDATING THE APPLICATION**

Codewind watches for file changes and automatically updates your application. If you edit `app.js` to change the "Hello from Appsody!" string, you can refresh your browser to see the text update straight away.

**>>>>>>>>>>>>>> ADD SUE's STOPPING THE APPLICATION - add something here**


You are now ready to develop your own app!

#### Developing and testing your app

As you progress with developing your app in VS Code, you are likely to want to do some local testing. As well as checking whether your code runs cleanly, you can also look at application metrics and performance monitoring.

##### Viewing application metrics

Right-click on the running project in the **CODEWIND** folder and select **Open Application Monitor** to open the  dashboard. Graphical information is displayed about CPU, Memory, and HTTP trafic.

##### Viewing performance monitoring

Right-click on the running project in the **CODEWIND** folder and select **Open Performance Dashboard**, which allows you to run load tests.


**>>>>>>>>>>>>>> SUE's DEPLOYING TO K8S**

#### Deploying your app on a local Kubernetes cluster

**>>>>>>>>>>>>>> SUE's DEPLOYING TO KNATIVE**

#### Deploying to KNative

**>>>>>>>>>>>>>> SUE's DELIVER TO ENTERPRISE PIPELINES**

#### Delivering your app to your Enterprise production environment

- Check in your changes to GitHub

Todd:
- Production OKD / OCD environment set up with appropriate pipelines
- Application (Project) is rebuilt and deployed to production
