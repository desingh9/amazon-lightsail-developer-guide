# Pushing and managing container images on your Amazon Lightsail container services<a name="amazon-lightsail-pushing-container-images"></a>

 *Last updated: November 12, 2020* 

When you create a deployment in your Amazon Lightsail container service, you must specify a source container image for each container entry\. You can use images from a public registry, such as Amazon ECR Public Gallery or Docker Hub, or you can use images that you create on your local machine\. In this guide, we show you how to push container images from your local machine to your Lightsail container service\. For more information about creating container images, see [Creating container images for your Amazon Lightsail container services](amazon-lightsail-creating-container-images.md)\.

**Contents:**
+ [Prerequisites](#push-container-images-prerequisites)
+ [Push container images from your local machine to your container service](#push-container-images)
+ [View container images stored on your container service](#view-pushed-container-images)
+ [Delete container images stored on your container service](#delete-stored-container-images)
+ [Additional information about container services](#pushing-container-images-additional-info)

## Prerequisites<a name="push-container-images-prerequisites"></a>

Complete the following prerequisites before you get started with pushing your container images to your container service:
+ Create your container service in your Lightsail account\. For more information, see [Creating Amazon Lightsail container services](amazon-lightsail-creating-container-services.md)\.
+ Install software on your local machine that you need to create your own container images and push them to your Lightsail container service\. For more information, see [Installing software to manage container images for your Amazon Lightsail container services](amazon-lightsail-install-software.md)\.
+ Create container images on your local machine, that you can push to your Lightsail container service\. For more information, see [Creating container images for your Amazon Lightsail container services](amazon-lightsail-creating-container-images.md)\.

## Push container images from your local machine to your container service<a name="push-container-images"></a>

Complete the following procedure to push your container images to your container service\.

1. Open a command prompt or terminal window\.

1. In the command prompt or terminal window, enter the following command to view the Docker images that are currently on your local machine\.

   ```
   docker images
   ```

1. In the result, locate the name \(repository name\) and tag of the container image that you want to push to your container service\. Make a note of it because you will need it in the next step\.  
![\[Docker container images on a local machine\]](https://d9yljz1nd5001.cloudfront.net/en_us/cdafd3c2a6d9edfefee89eda217b0068/images/amazon-lightsail-container-service-docker-images.png)

1. Enter the following command to push the container image on your local machine to your container service\.

   ```
   aws lightsail push-container-image --region <Region> --service-name <ContainerServiceName> --label <ContainerImageLabel> --image <LocalContainerImageName>:<ImageTag>
   ```

   In the command, replace:
   + *<Region>* with the AWS Region in which your container service was created\.
   + *<ContainerServiceName>* with the name of your container service\.
   + *<ContainerImageLabel>* with the label that you want to give your container image when it's stored on your container service\. Specify a descriptive label that you can use to track the different versions of your registered container images\.

     The label will be part of the container image name generated by your container service\. For example, if your container service name is `container-service-1`, the container image label is `mystaticsite`, and this is the first version of the container image you're pushing, then the image name generated by your container service will be `:container-service-1.mystaticsite.1`\.
   + *<LocalContainerImageName>* with the name of the container image that you want to push to your container service\. You obtained the container image name in the previous step of this procedure\.
   + *<ImageTag>* with the tag of the container image that you want to push to your container service\. You obtained the container image tag in the previous step of this procedure\.

   Example:

   ```
   aws lightsail push-container-image --region us-west-2 --service-name myservice --label mystaticwebsite --image mystaticwebsite:v2
   ```

   You should see a result similar to the following example, which confirms that your container image was pushed to your container service\.  
![\[Docker container image pushed to a Lightsail container service\]](https://d9yljz1nd5001.cloudfront.net/en_us/cdafd3c2a6d9edfefee89eda217b0068/images/amazon-lightsail-container-service-pushed-image.png)

   Refer to the following [View container images stored on your container service](#view-pushed-container-images) section of this guide to view your pushed container image in your container service on the Lightsail console\.

## View container images stored on your container service<a name="view-pushed-container-images"></a>

Complete the following procedure to view container images that were pushed, and are being stored, on your container service\.

1. Sign in to the [Lightsail console](https://lightsail.aws.amazon.com/)\.

1. On the Lightsail home page, choose the **Containers** tab\.

1. Choose the name of the container service for which you want to view the stored container images\.

1. On the container service management page, choose the **Images** tab\.
**Note**  
The **Images** tab is not displayed if you have not pushed images to your container service\. To display the images tab for your container service you must first push container images to your service\.

   The **Images** page lists the container images that were pushed to your container service, and are currently being stored on your service\. Container images that are being used in a current deployment cannot be deleted and are listed with a grayed\-out delete icon\.  
![\[The stored images page of the Lightsail console\]](https://d9yljz1nd5001.cloudfront.net/en_us/cdafd3c2a6d9edfefee89eda217b0068/images/amazon-lightsail-container-services-stored-images-page.png)

   You can create deployments using container images stored on your service\. For more information, see Creating and managing deployments for your Amazon Lightsail container services\.

## Delete container images stored on your container service<a name="delete-stored-container-images"></a>

Complete the following procedure to delete container images that were pushed, and are being stored, on your container service\.

1. Sign in to the [Lightsail console](https://lightsail.aws.amazon.com/)\.

1. On the Lightsail home page, choose the **Containers** tab\.

1. Choose the name of the container service for which you want to view the current deployment\.

1. On the container service management page, choose the **Images** tab\.
**Note**  
The **Images** tab is not displayed if you have not pushed images to your container service\. To display the images tab for your container service you must first push container images to your service\.

1. Find the container image you want to delete, and choose the delete \(trash bin\) icon\.
**Note**  
Container images that are being used in a current deployment cannot be deleted and their delete icons are grayed\-out\.

1. In the confirmation prompt that appears, choose **Yes, delete** to confirm that you want to permanently delete the stored image\.

   Your stored container image is immediately deleted from your container service\.

## Additional information about container services<a name="pushing-container-images-additional-info"></a>

These are the general steps to manage your Lightsail container service after it's up and running:

1. Get familiar with all of the elements of Lightsail container services\. For more information, see [Container services in Amazon Lightsail](amazon-lightsail-container-services.md)\.

1. Create your container service in your Lightsail account\. For more information, see [Creating Amazon Lightsail container services](amazon-lightsail-creating-container-services.md)\.

1. If you plan to use container images from a public registry, find container images that you want to use from a public registry like the Amazon ECR Public Gallery or Docker Hub\. For more information about Amazon ECR Public, see [What Is Amazon Elastic Container Registry Public?](https://docs.aws.amazon.com/AmazonECR/latest/public/what-is-ecr.html) in the *Amazon ECR Public User Guide*\. For more information about Docker Hub, see [Docker Hub Quickstart](https://docs.docker.com/docker-hub/) in the *Docker documentation*\.

1. If you plan to push container images from your local machine to your service, install software on your local machine that you need to create your own container images and push them to your Lightsail container service\. For more information, see the following guides:
   + [Installing software to manage container images for your Amazon Lightsail container services](amazon-lightsail-install-software.md)
   + [Creating container images for your Amazon Lightsail container services](amazon-lightsail-creating-container-images.md)
   + [Pushing and managing container images on your Amazon Lightsail container services](#amazon-lightsail-pushing-container-images)

1. Create a deployment in your container service that configures and launches your containers\. For more information, see [Creating and managing deployments for your Amazon Lightsail container services](amazon-lightsail-container-services-deployments.md)\.

1. View previous deployments for your container service\. You can create a new deployment using a previous deployment version\. For more information, see [Viewing and managing deployment versions of your Amazon Lightsail container services](amazon-lightsail-container-services-deployment-versions.md)\.

1. View the logs of containers on your container service\. For more information, see [Viewing the container logs of your Amazon Lightsail container services](amazon-lightsail-viewing-container-service-container-logs.md)\.

1. Create an SSL/TLS certificate for the domains that you want to use with your containers\. For more information, see [Creating SSL/TLS certificates for your Amazon Lightsail container services](amazon-lightsail-creating-container-services-certificates.md)\.

1. Validate the SSL/TLS certificate by adding records to the DNS of your domains\. For more information, see [Validating SSL/TLS certificates for your Amazon Lightsail container services](amazon-lightsail-validating-container-services-certificates.md)\.

1. Enable custom domains by attaching a valid SSL/TLS certificate to your container service\. For more information, see [Enabling and managing custom domains for your Amazon Lightsail container services](amazon-lightsail-enabling-container-services-custom-domains.md)\.

1. Monitor the utilization metrics of your container service\. For more information, see [Viewing container service metrics in Amazon Lightsail](amazon-lightsail-viewing-container-services-metrics.md)\.

1. \(Optional\) Scale the capacity of your container service vertically, by increasing its power specification, and horizontally, by increasing its scale specification\. For more information, see [Changing the capacity of your Amazon Lightsail container services](amazon-lightsail-changing-container-service-capacity.md)\.

1. Delete your container service if you're not using it to avoid incurring monthly charges\. For more information, see [Deleting Amazon Lightsail container services](amazon-lightsail-deleting-container-services.md)\.