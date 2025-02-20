 HL-PreAssessment

# Backend Questions

### Answer of Question 1.


For an overview of the system follow the question I think it have architecture follow Fig. 1.1 below. The system consists of 3 microservices: customer service, master data service, and transaction data service. And each microservices have own database. When an external request is received, it is first handled by the API Gateway. This setup aligns with the microservices architecture pattern [https://microservices.io/patterns/microservices.html](https://microservices.io/patterns/microservices.html)) .

To provide API for display data from 3 microservices above nearly real-time. My solution is design adds a new microservices named "Data Aggregate Service" to handle aggregate data from the 3 microservices above by get data via message broker and return data aggregated back to the client. For the nearly real-time provided data aggregated necessary to have caching data at the Data Aggregate Service.

![architecture diagram](https://res.cloudinary.com/dmdxfjunb/image/upload/v1720244389/HLAB-Architecture_Diagram_oopsbw.jpg) \
Fig. 1.1: Architecture diagram 

The component of each microservices is follow the class diagram in Fig. 1.2 below. API Gateway has the APIGatewayController class which routes the request to internal microservices. All internal microservices consisting of controller class handle request, service class handle about business logic as same as. However 3 microservices: customer service, master data service, and transaction data services have entity classes of data that each microservice owns. Every microservices and API gateway has the authorization class with concern about the security of the system.

![class diagram](https://res.cloudinary.com/dmdxfjunb/image/upload/v1720244482/HLAB-Class_Diagram_nkw46w.jpg) \
Fig. 1.2: Class diagram 

When have a request to get customer data, master data, and transaction data. Begin The collaboration between the API gateway and each microservice follows the sequence diagram in Fig. 1.3 below. The request is sent to the API gateway first and authorized request by using the userId and token from the request. If the access type is true, the request and parameters like userId and token are sent to the data aggregate service. Before the data aggregate service executes must be authorized by using userId and token same. Next, the operation executed by DataAggregateService starts with call data from the cache. If the cache does not have the data, the service must have call data from  3 microservices via message broker by using a message pattern. Finally, after calling all data successfully the service just aggregates data before saving the data to the cache and return to the client

![sequence diagram](https://res.cloudinary.com/dmdxfjunb/image/upload/v1720244488/Untitled_19_sylyvk.png) \
Fig. 1.3: Sequence diagram 

Finally, the client can call API to get all data with API path name /getDataAggregated and must send the parameter userId and token within the request.


------------------------------------------------

### Answer of Question 2.
I want descrip this issues with activity diagram shows in Fig 2.1. Which consists of defining the objective, identifying the scope, creating a test plan, selecting tools, executing, analyzing, reporting, and optimizing software. The details are as follows:
1. Define performance test objective 
Form non-functional requirement can identify the Objective and criteria of performance testing. What is the aspect of test like speed, response time, load, resource usage, or stability? And define the criteria of each aspect. This process output is the test objective and criteria.
2. Identify scope
Identify which components, modules, and integrations will be tested. This process output is the test scope.
3. Create test plan
Design performance test cases of each scenario. Plan sequence and timing of test case by concern about coverage and config of test case. This process output is a test case and schedule.
4. Select test tools
Select tools for performance testing in each aspect of testing like Gatling([https://docs.gatling.io/tutorials/scripting-intro-js/](https://docs.gatling.io/tutorials/scripting-intro-js/)), LoadRunner([https://www.opentext.com/en-gb/products/loadrunner-professional](https://www.opentext.com/en-gb/products/loadrunner-professional)), JMeter([https://jmeter.apache.org](https://jmeter.apache.org)), and etc.
5. Execute test
From the test case, test plan, and test tool execute the performance test and collect the test result. In this process, the output is the test result.
6. Analyze and reports
Compare actual performance with criteria of testing. Identify issues of performance to be optimized. Develop a report of performance test.
7. Optimize 
If the performance test result is not good or does not pass criteria can optimize the software and re-testing.

![sequence diagram](https://res.cloudinary.com/dmdxfjunb/image/upload/v1720288294/HLAB-performance_test_wcog4q.jpg) \
Fig. 2.1: Activity diagram of performance testing



