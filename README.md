# HL-PreAssessment

## Backend Questions

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


