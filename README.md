# ANSIBLE-DYNAMIC-ASSIGNMENTS-INCLUDE-AND-COMMUNITY-ROLES

In this project we will introduce dynamic assignments by using include module.By dynamic, it means that all statements are processed only during execution of the playbook which is the opposite of the import modules.

The following steps outlines how include module is used for running dynamic environment variable:

I create a new folder, named it ' dynamic-assignments '. Then inside this folder, created a new file and named it ' env-vars.yml ' .

![ta1](https://user-images.githubusercontent.com/94229949/204675573-a6351919-7874-4cbd-afe3-0350f0f25259.png)

Since I will be using the same Ansible to configure several environments, each of which will have distinct features such as servername, ip-address, and so on, I will need a way to set values to variables per environment.

As a result, I created a folder to store each environment's variables file.  I created a new folder called env-vars, and then for each environment, I created new YAML files that we would use to set variables.



This is how the layout should now look.

![tar2](https://user-images.githubusercontent.com/94229949/204676770-6d9d9c47-3d33-470b-9d33-828740b0a9b2.png)

I entered the following instructions into the env-vars.yml file.

![ta16](https://user-images.githubusercontent.com/94229949/204678803-dafa624c-7bde-45fb-b6c4-67466f530f9d.png)


Updated site.yml file to work with dynamic-assignments

![ta17](https://user-images.githubusercontent.com/94229949/204683155-329983f6-d011-4746-a979-531c7aa834dc.png)

Inside roles directory I created a new MySQL role with ' ansible-galaxy install geerlingguy.mysql ' and renamed the folder to mysql


![ta5](https://user-images.githubusercontent.com/94229949/204683749-f8294f25-b57d-49da-befd-0af5a388bc81.png)

![ta6](https://user-images.githubusercontent.com/94229949/204683761-a02224bd-d382-4a7e-807a-070aab5da636.png)

![ta9](https://user-images.githubusercontent.com/94229949/204683784-814008fb-ba64-4a8d-b23d-c35134537034.png)

Uploaded the changes into GitHub

![ta8](https://user-images.githubusercontent.com/94229949/204684082-bbe90bbb-e24f-4d80-a9c5-e20808eb31a0.png)

I want to be able to select which Load Balancer to utilise, Nginx or Apache, hence I needed two roles. Because I cannot utilise both Nginx and Apache load balancers, I must add a condition to activate either one - this is where I use variables .

Declared a variable in defaults/main.yml file inside the Nginx and Apache roles. Named each variables ' enable_nginx_lb ' and ' enable_apache_lb '.

Set both values to false: ' enable_nginx_lb: false' and ' enable_apache_lb: false ' .

Declared another variable in both roles: load_balancer_is_required and set its value to false as well


![ta11](https://user-images.githubusercontent.com/94229949/204685864-a3ac4a8e-ff44-4eae-adb7-b748e5692a81.png)

![ta12](https://user-images.githubusercontent.com/94229949/204685879-db41960a-e8c6-4a81-8021-85a9bf5e719f.png)


Created a file in static-assignments folder named loadbalancer.yml. I entered the following instructions into the loadbalancer.yml file and updated site.yml file.

![ta18](https://user-images.githubusercontent.com/94229949/204687239-bb5d9d2b-b37e-498a-bcce-ddd75a092519.png)

![ta19](https://user-images.githubusercontent.com/94229949/204687576-f7608e68-2b4e-4f86-b0e8-f5f0c8517514.png)

I can make use of env-vars\uat.yml file to define which loadbalancer to use in UAT environment by setting respective environmental variable to true.

I will activate load balancer, and enable nginx by setting these in the respective environment’s env-vars file.

![ta20](https://user-images.githubusercontent.com/94229949/204688250-23d70c99-bcff-4e0f-bf3e-cddf9493865e.png)

The same must work with apache LB, so i can switch it by setting respective environmental variable to true and other to false.

Then i ran the playbook. 

![ta22](https://user-images.githubusercontent.com/94229949/204692423-8f46a677-b9da-4e2a-9c64-927071f2fef2.png)

![ta23](https://user-images.githubusercontent.com/94229949/204692438-d5532305-63fc-44cc-bd93-3fc49ddf794c.png)

![ta24](https://user-images.githubusercontent.com/94229949/204692450-7b1e7404-cf80-4cfd-b67c-11cfa8e150a8.png)

![ta25](https://user-images.githubusercontent.com/94229949/204692479-b015c156-beb7-4a7d-8c19-346cf9a168d7.png)

















