This project uses Entity Framework Core, Code First and migrations. This section is intended to answer and explain common practices.

Migration work is mostly done in the Package Management Console. You can open the PMC from the Tools Menu.

![image.png](/.attachments/image-1dd2beec-ce9c-4132-8c61-fa8a1cd44d95.png)

Because this project is use a n-tier architecture Entity Framework resides in the `*.DAL.SQL` project. In order to use the commands in the rest of the tutorial you will need to set the context in the PMC.

![image.png](/.attachments/image-705a2845-e594-4c7b-a36e-8ec9f0576511.png)