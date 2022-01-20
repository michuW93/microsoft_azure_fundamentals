# microsoft_azure_fundamentals-AZ-900-
Tutorial based on Vlad Catrinescu and Neil Morrissey tutorial


# Introduction to cloud computing
In past each company got tons of servers for different purposes. They could run on different hardware, different operating systems. Each server got it's own RAM, CPU etc.
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/old_servers.png?raw=true)

Problems: 
* a lot of money 
* often servers were under utilized (e.g take only 20% of servers resources)
* for safety in case of disaster e.g flood, fire company need two serverrooms in different part of the world

then we switch to <b>virtualization</b>:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/virtualization.png?raw=true)

it was cheaper, needed less space but still got some disadventages - high up-front cost, need space in datacenter, need to pay for electricity

then we have <b>cloud computing</b> - Cloud computing enables companies to consume a compute resource rather than having tobuild and maintain computing infrastructures in house, it's like buying electricity, not building power station:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/cloud_computing.png?raw=true)

Cloud provider owns data center and manages servers, networking, virtualization etc.
All those resorces are shared between many clients, clients don't know which server is their, all they care is that they have enought resorces which cloud provider guarantee.

Cloud infrastructure is on demand self-service - you pay for using resources. Usually it's paid for seconds, minutes or hours. Azure is charging for seconds - your app worked 35secs, you pay for 35secs.

When you order Microsoft Azure you choose in which region server should be, which oparating system you want, how many RAM you need, how many CPU, how many storage and if it should be scaled on demand or automatically. Automatically mean that if CPU usage goes to 70% it can automatically add another CPU e.g when a lot of people want to use your website it will scale automatically and allow server to not go down. You'll pay a bit more for this time and then when additional CPU won't be needed anymore it will be taken away. It's called rapid elasticity. 

Cloud computing reliability - cloud provider take care about high availibility (HA) and disaster recovery (DR). High availibility is eg. power supply, disk failure etc. Disaster recovery is fire, flood, earthquake. Fault tolerance - zero downtime. If you would implement disaster recovery yourself you would need another data center so if your first datacenter is in Manila (capital of Philippines) then your second datacenter can be in Minsk (the capital of Belarus) or e.g Podgorica (the capital of Montenegro). With cloud provider you benefit from scale because cloud providers already have it. Azure datacenters are in 60 regions world wide.

Conclusion:
* allows organisations to consume computing resources as utility
* rapid elasticity
* billed per second/minute/hour
* reliability
* economies of scale

# Types of Cloud Computing Services
Infrastructure as a Service(IaaS), Platform as a Service(PaaS) and Software as a Service(SaaS)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/on_premise_iaas_paas_saas.png?raw=true)

comparing to pizza:
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/pizza_as_a_service.png?raw=true)


Most popular cloud providers:
* IaaS: Microsoft Azure, Amazon Web Services, Google Compute Engine
* Paas: Azure Logic Apps, Heroku, Amazon Elastic Beanstalk
* Saas: Office 365, Salesforce, Dropbox

Cloud Computing Services by Microsoft:
* IaaS: Azure Compute, Azure Storage
* PaaS: Azure Logic Apps, Azure Functions, Azure Web Jobs, Azure Automation
* SaaS: SharePoint, OneDrive for Business, Microsoft Teams, Power Platform


<b>Infrastructure as a service</b>:
perfect for test and development scenarios because you can turn on and turn off dev machines only when needed so you dont need to pay all the time.
Storage and backups as price is good. High performance computing and data analyzis - require very powerful computers for a short time.

<b>Platform as a service:</b>
analytics or business inteligence - alows company to analyze and mine data finding insights and patterns and predict outcomes to improve forecasting, product design decisions etc. it's also great for developers.

<b>Software as a service:</b>
getting access to sophisticated applications and no need to manage any infrastructure yourself. Imagine all of the work needed to install Skype for business, SharePoint servers on premises vs just using the same tools in a matter of minutes.

# Cloud computing deployment models
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/Cloud_Computing_Deployment_Models.png?raw=true)

<b>Public Cloud</b>
Multiple clients, shares hardware and backend. Most Azure customers are in public cloud.

<b>Private cloud</b>
Hardware used by a single company, usually (but not necesairly) who owns the datacenter. Close to traditional way. Azure Stack allows you to run cloud services on-premises. Later you can easily transfer to public cloud

<b>Hybrid cloud</b>
combination of public and private cloud with automation and orchestration betweeen them.Azure Stack allows you to run cloud services on-premises. Later you can easily transfer to public cloud

<b>Community cloud</b>
Infrastructure is shared between serveral organizations from a specific community with common concerns e.g security, compliance, jurisdiction. The most popular example is <b>Azure Goverment</b> - Azure offering specific to a government entities. To register for Azure Govenment you need to be validated as government organization. It's hosted in separate datacenters from public cloud.

# Azure data centers
Azure is just bunch of physical data centers full of physical servers. They locations are not public, often even Microsoft employees don't know locations. 

# Azure regions
for some Azure services you don't choose location, they are global (non-regional) but for most of them you need to specify in which region your account/storage etc. should be created. When you e.g work in Rotterdam (where is the biggest seaport in Europe) then it's better to choose some place in Europe for server location than e.g some place on smallest continent on the world - Australia because all requests would go from Rotterdam to Canberra (capital of Australia) and responses from Canberra to Rotterdam and it takes time. We need to remember not all services are available in all locations. 

Azure provide Regions Pairs - it means your data can be duplicated between two locations in case of failury of one data center or natural disaster. We don't decide what regions are paired, Microsoft do it.
