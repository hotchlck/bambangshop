# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [x] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [x] Commit: `Create Subscriber model struct.`
    -   [x] Commit: `Create Notification model struct.`
    -   [x] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [x] Commit: `Implement add function in Subscriber repository.`
    -   [x] Commit: `Implement list_all function in Subscriber repository.`
    -   [x] Commit: `Implement delete function in Subscriber repository.`
    -   [x] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [x] Commit: `Create Notification service struct skeleton.`
    -   [x] Commit: `Implement subscribe function in Notification service.`
    -   [x] Commit: `Implement subscribe function in Notification controller.`
    -   [x] Commit: `Implement unsubscribe function in Notification service.`
    -   [x] Commit: `Implement unsubscribe function in Notification controller.`
    -   [x] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [x] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [x] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [x] Commit: `Implement publish function in Program service and Program controller.`
    -   [x] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [x] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1
1. If we aim to incorporate a variety of methods or distinct behaviors for different customer types, it’s crucial to establish a customer interface. 
However, if all customers are expected to exhibit the same behaviors and methods, a single Model structure would suffice.

2. Vec might not be the best choice if an attribute needs to be unique, as Vec doesn’t automatically guarantee element uniqueness. 
In this case, DashMap, which has already been implemented, is a better option because it ensures key uniqueness and prevents URL duplication. 
With DashMap, each element is unique in the data structure because when an existing key is inserted, its value is updated with the new one.

3. Direct implementation of the Singleton pattern can also ensure thread safety for the program, provided it’s correctly implemented. 
However, it’s more advisable to use DashMap, a pre-built library with guaranteed thread safety, as it eliminates the need for us to implement it ourselves.

#### Reflection Publisher-2
1. The division of tasks between the Model, Service, and Repository is crucial to ensure that the Model does not handle all responsibilities alone, but also shares them with the Service and Repository according to their respective functions. This division allows the application to adhere to clean code principles and the Single Responsibility Principle, making the code easier to maintain and update.

2. If an application only uses the Model, all responsibilities will be handled by the model, making the code for each model more complex and lengthy. The code will manage requests and responses, data container structures, contain methods for business logic, and act as a database with methods for accessing it. In short, all tasks of each MVC component will be handled by the Model’s code.

3. I have been using Postman since the third semester. I typically use this application to test the functionality of applications by sending requests and checking the responses returned by the application.The user-friendly GUI of Postman is its main advantage. The ability of Postman to export and import allows us to send tests quickly.

#### Reflection Publisher-3
1. The observer type used in this tutorial is push. 
This is evident from the role of the publisher as an active actor sending data to its users.

2. The advantage of using pull in Observer is to reduce the dependency between the observer and the subject, allowing more flexibility
However, the downside is that it can increase complexity in managing the observer.

3. This will eliminate the real-time characteristic because the notification process is done sequentially. 
This effect will be very noticeable if the number of observers is very large.
