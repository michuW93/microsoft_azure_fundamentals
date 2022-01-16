# microsoft_azure_fundamentals-AZ-900-
Tutorial based on Vlad Catrinescu tutorial


# Introduction to cloud computing
In past each company got tons of servers for different purposes. They could run on different hardware, different operating systems. Each server got it's own RAM, CPU etc.
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals-AZ-900-/blob/master/old_servers.png?raw=true)

Problems: 
* a lot of money 
* often servers were under utilized
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
