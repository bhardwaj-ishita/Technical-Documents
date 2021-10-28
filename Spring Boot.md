# Spring Boot:

1. **Display Layer:** It's the front layer or upper layer of this structure, as it is made up of viewpoints.  It's used to interpret the JSON areas to items and vice-versa and handles authentication and HTTP requests.  After finishing the authentication, it moves into the business layer for additional processes. 
2. **Business Layer:** It manages all of the business logic and performs validation and consent since it's part of business logic.  By way of instance, only admins are permitted to alter the consumer's account.
3. **Persistence Layer:** It comprises all of the storage logic, such as database questions of this program. Additionally, it translates the company items from and to database rows.
4. **Database Layer:** It could include many databases. The execution of the aforementioned layered structure is performed in this way: The HTTP request or internet requests are managed by the Controllers from the demonstration layer, the providers control the company logic, as well as also the repositories handle persistence (storage logic). A control can manage numerous providers, a service may manage many repositories, and also a repository may manage many databases.

![image-20210613224033851](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210613224033851.png)

The first component is the **Spring Boot starter component** which handles the dependency management. Using this component one can resolve the problem as this provides a set of dependencies made exclusively for programmers’ convenience. For example, if one needs to include all dependencies required for security, they can use spring-boot-starter-security as the artifact-id. The required dependencies are mentioned in pom.xml.

Next in line is the **auto-configuration** using *@EnableAutoConfiguration* or *@SpringBootApplication* and these annotations help in automatically configuring the spring boot application being developed. For example, if there is the presence of the MySQL database in the classes defined in the application, then this autoconfiguration will configure an in-memory database.

To have an entry point in our code for the spring boot application we use the annotation *@SpringBootApplication*.

