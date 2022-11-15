### Softwares necessary to run it

- [Serverless Framework & Localstack plugin](https://www.npmjs.com/package/serverless-localstack "Serverless") (**just necessary execute the first step "Installation"**)
- [Docker & Docker-compose](https://docs.docker.com/compose/install/ "Docker-compose")

### Steps to run it

- Unzip the folder and go to directory localstack-env
- Run the command below:
  - `$ docker-compose up -d`
- After containers are up you can deploy the API Gateway and Lambda function throught the command:
  - `$ serverless deploy --stage local`
- After it has been deployed an endpoint will be printed on console as shown on the image below, please **copy** it (it's our API gateway endpoint).
  
  ![](https://github.com/JonataSaraiva/temp/blob/main/endpoint.png)
- After we have finished our infrastructure configuration we need to up our applications. For our 3 microservices the step is the same. You can use a IDEA to download maven dependencies and after that execute the main class to up the app.

### Testing it
After has everything running we can execute some requests. You can find a postman collection in the folder **postman**, it's necessary just replace the endpoint for the new one that you've copied before.

**FYI**: There is a JMeter test plan in the folder **jmeter** too. I have used it to accomplish the requirement of 3 simultaneous devices sending requests to the API.

#### Authentication
For execute a request in the API-Query is necessary sending a header called **Token** with the value **1234567**, it's just to exemplify how the security validation could be done. ( At V1 architecture I hava exemplified a new strategy using a call for a OAuth Service )

### Technical debts & Improvements
- Improve the unit test coverage
- add integration test
- change some hardcode variables to env variables (SQS queue, App address and anothers)
- add validations to the api ( bean validation to guarantee that our app is receiving the right values )
- add exception handler to handle exceptions and delivery better messages to client.
- improve the scenario where a name/group with no registries on db is sent to the query API (it's answering some negative values)
