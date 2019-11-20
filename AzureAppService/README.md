**StreamSets DataCollector:**

**Create StreamSets DataCollector as Azure App Service**

In this tutorial, we will explain how StreamSets DataCollector (SDC) is deployed as an Azure App Service while persisting the pipelines over SDC restarts. 

To recap, other way to install SDC are:



*   Tarball
*   RPM Package
*   Docker
*   AWS marketplace
*   Azure marketplace

Although, Azure App Services persist the state of an app during execution mode, they do not store the state over a restart. Meaning, after every single SDC restart all pipelines will be lost each time. 

Due to the stateless nature of App Services, relevant directories must be stored outside of the App Service while being permanently accessible by the App.

For SDC that will require to create external containers and mount them to the paths that need to be stateful.

In SDC (at least this folder):

/data

Other folders can be also mounted to Azure containers.

This approach will allow to keep and persist pipelines over multiple restarts and across the entire lifetime of the App Service.



1. Create SDC as App Service
    1. **Add**.

        

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Azure-App0.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Azure-App0.png "image_tooltip")


    2. After adding app service name, resource group, app service plan click on **Next**.
    3. Choose for Image Source = Docker Hub

        Image and tag = streamsets/datacollector:latest. Alternatively, choose your own derived Docker DataCollector image.


        

<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Azure-App1.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Azure-App1.png "image_tooltip")


    4. Complete the creation of the App Service.
2. Create Azure storage container
1. Go to your storage account and add a container.

<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Azure-App2.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Azure-App2.png "image_tooltip")

2. Add the container name and choose public access-type = Blob.

        

<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Azure-App3.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Azure-App3.png "image_tooltip")


3. Mount SDC paths to Azure Containers.
1. Go to the App Service -> **Configuration** -> **Path mappings**.

<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Azure-App4.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Azure-App4.png "image_tooltip")

2. Add “New Azure Storage Mount”.

<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Azure-App5.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Azure-App5.png "image_tooltip")

3. Click **Ok** .

<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Azure-App6.png). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Azure-App6.png "image_tooltip")

4. Restart App Service.

_Note:_

_In case, you need to install in the SDC App Service additional SDCs libraries (connectors, processors etc.), we recommend to create a custom SDC docker image containing the additional SDCs libraries. Then, deploy the custom SDC docker image as an Azure App Service and mount /data, /log and other folders to the Azure Containers._

<h4>**Conclusion**</h4>


This blog post highlighted how to create StreamSets DataCollector as an Azure App Service and persist pipelines over multiple restarts.

