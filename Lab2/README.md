# Lab2

The task for Lab2 is to build an Azure DevOps pipeline using a Node.js example. 

## Link to the web application repository

https://github.com/tamara201/Software-Deployment-Lab2-WebApp

## Azure Web Apps

[Web App for development](https://117939lab2-dev.azurewebsites.net/) \
[Web App for production (release)](https://117939lab2-release.azurewebsites.net/)

## Screenshots

### Build

![build](https://github.com/tamara201/test-lab2/blob/main/images/build.png)

### Deploy

![deploy](https://github.com/tamara201/test-lab2/blob/main/images/deploy.png)

### Deployments

![deployments](https://github.com/tamara201/test-lab2/blob/main/images/deployments.png)

### Release Pipeline

![release pipeline](https://github.com/tamara201/test-lab2/blob/main/images/release_pipeline.png)

After commiting to the main branch of the repository, a new release will be triggered. First, the pipeline will build the WebApp and run the tests. After all tests pass, the changes have to be approved. If the changes are approved the app will be deployed.

## Personal experience

I had no proplems creating a simple WebApp ([tutorial](https://expressjs.com/en/starter/installing.html)). However, I run into proplems while working with Azure DevOps. First of all, I had to move my WebApp to a seperate repository because it has to be in the same repository as the **azure-pipelines.yml** file. Simple changing the path of the app in the pipeline file did not work. Furthermore, I also had to change the script of the **azure-pipelines.yml** file and I added a test and build script to the node.js app in order to succesfully deploy. Moreover, with the help of this [tutorial](https://www.youtube.com/watch?v=BAFCiiOAXB8) I created the release pipeline. Lastly, I also added Azure Application Insights to my application.
