1. Introduction
    Thusfar we have only worked in the browser (in angular). This means any we control all our data with Angular. A page loads and all our data is gone. We can't persist data anywhere. In any real project, our App would need to communicate with a server to store and fetch data, or anything else that needs to be done.

    We will learn how Angular connects to back-ends, send HTTP requests and how to transform data if required. See the Observables section.

2. How Does Angular Interact with Backends?

    Angular is built to store and fetch data from databases. doesn't matter if it's SQL or noSQL. Angular doesn't directly connect to databases, we do not enter database credentials into the angular app. That would be very bad because everyone can simply read that information off of the HTML page.

    Instead your Angular app should make HTTP requests and get HTTP responses through an API, an Application Programming Interface, (i.e. a REST API or a GraphQL API) in this course we'll use RESTAPI as it is the most common API.
    When you visit an API URL you are not getting HTML back but data in the JSON format. You can learn more about it in the NodeJS course, where you will learn about NodeJS or PHP.
    this API could then access data from the database for you.
    API use isn't just about databases, it can also be used to upload files, send analytics to back-end.

3. The Anatomy of a Http Request

    HTTP Verb -> POST, GET, PUT, ...
        the Verb tells that request what is being done, whether collecting data, adding, or replacing data

    URL (API Endpoint)  -> /posts/1
        the location of the data you are interacting with

    Headers (Metadata)  -> {"Content-Type": "application/json"}
        Optional, there are default headers and they can be changed
    
    Body -> {title: "New Post"}
        Some Verbs can have a body, such as POST, PUT, PATCH that lets the request know what to add, or replace.

4. Backend (Firebase) Setup

    Max's Mean course 

    Firebase sounds like a database only, but it is a whole back-end solution that gives us a RESTAPI. It's perfect because it's free to get started with and we can send requests, see different kinds of requests and store data there. Log in with a Google Account


5. Sending a POST Request

    in the app.module HttpClientModule needs to be imported from '@angular/common/http' and added to the @NgModule({imports: []}) array. Ex:
        import { HttpClientModule } from '@angular/common/http';

    the HttpClientModule provides several methods callable with this.http. Ex:

    .post('specific url endpoint', data) uploads data

    Firebase's API allows you create new folders with custom endpoints. This is not direct connection to the Database, it is an API connection, a direct database connection is very insecure. Adding .json to the end of the request body.

    http.Post returns an observable that accesses the request, if you arent subscribing to it, then Angular and RxJS know that no-one is interested in the response, so the request isn't sent.

    onCreatePost(postData: { title: string; content: string }) {
        this.http
        .post(
            'URL',
            postData
        )
        .subscribe(responseData => {
            console.log(responseData);
        })
    }
6. GETting Data


7. Uing RxJS Operators to Transform Response Data


8. Using Types with the HttpClient


9.  Outputting Posts


10. Showing a Loading Indicator


11. Using a Service for Http Requests


12. Services & Components Working Together


13. Sending a DELETE Request


14. Handling Errors


15. Using Subjects for Error Handling


16. Using the catchError Operator


17. Error Handling & UX


18. Setting Headers


19. Adding Query Params


20. Observing Different Types of Responses


21. Changing the Response Body Type


22. Introducing Interceptors


23. Manipulating Request Objects


24. Response Interceptors


25. Multiple Interceptors


26. Wrap Up
27. 