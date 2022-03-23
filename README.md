# ase-delivery
ASE Delivery is a logistics system. ASE Delivery software manages the lifecycle of a delivery package from the point it is picked up by the deliverer from
the central depot to when the customer opens the box to retrieve their items.

For a more detailed explanation of the project please refer to the project description document in repository.

<img width="682" alt="Example diagram" src="https://user-images.githubusercontent.com/22833948/159519642-42228d4f-5fd4-436f-8643-4922e4a9a300.png">

## Lifecycle of a Delivery

![Lifecycle Diagram](https://user-images.githubusercontent.com/22833948/159519607-75f411ec-3c83-4fb8-83d2-4df035acb278.png)

## Components

<img width="830" alt="Container Diagram of system" src="https://user-images.githubusercontent.com/22833948/159523606-38f4484d-b4df-48c3-ad45-b39a66e9add2.png">

- Frontend Dashboard UI (React)
  - User role is determined after login
  - Dispatcher actions: Create Dispatcher/Deliverer/Customer, create delivery
  - Deliverer actions: Update delivery statuses to collected
  - Customer actions: View your current/past deliveries and their statuses
- ASE Delivery Hardware (Python/RBP)
  - Reads the RFID cards
  - Communicates with backend to check if the owner of RFID token has permission to open the box
  - Lights a green LED if deliverer/customer is authorized to open the lock. Otherwise lights red.
  - Uses photoresistor light sensor to detect if box is open
  - Blinks red LED if the box is not closed properly within 10 seconds
- API Gateway (Spring Boot/Spring API Gateway)
  - Communicates with the service registry to learn about services
  - Checks the JWTs for permission to access endpoints
  - Forwards the authorized requests to services
- Service Registry (Spring Boot/Spring Cloud Eureka)
  - Manages and keeps track of which services/machines are up and available
- Delivery Service (Spring Boot)
  - Creates and stores deliveries and boxes in MongoDB.
  - Responsible for managing the whole lifecycle of a delivery.
- Customer Authentication Service (Spring Boot)
  - Stores the users and their roles in MongoDB
  - Creates the JWTs for the users for authorization


## Technology Overview
- JS, React, MaterialUI
- Java, Spring Boot
- Spring Cloud: Spring API Gateway, Spring Cloud Eureka
- MongoDB
- Docker, docker-compose (see the docker-compose in ase-delivery-deployment repo)
- AWS (project was originally deployed to AWS by our GitLab CI process)
- GitLab CI/CD (.gitlab-ci.yml file and our CI process can be found in ase-delivery-deployment repo)
