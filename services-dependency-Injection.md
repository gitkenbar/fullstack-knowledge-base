1. Introduction
    What are Services?
        a class to duplicate code or store data. a central repository, a place to serve out code and data to multiple components.

2. Why would you need services

    Any time a script is re-used on multiple components.
    Any time data needs to be passed around to different components.

3. Creating a Logging Service

    Creating a service with the CLI:
        ng g s shared/ServiceName

    since components are declared with @component, and directives with @directives, you might think services are made with a @service decorator, but they are simply a normal typescript class.

    in a Typescript file:

    export class ServiceName {
        let property: type = ''

        method () {
            what the method does
        }
    }

    instantiating the service might look like this:

    const service = new LoggingService()
    service.logStatusChange(accountStatus);

    but angular had a better method, service Injection.

4. Injecting the Logging Service into Components

    a dependency is something our class will depend on. in the example project, the new account component depends on the logging service, since it calls a method from that service.

    To inform angular of the dependencies to be injected in a class, we use a constructor

    constructor(private LocalServiceName: ImportedServiceClassName) {}


    we need to tell angular how to give us what we want by using a provider, which we add to the @Component decorator meta-data object. i.e.

    @Component({
        ...
        providers: [ServiceName]
    })

    Services can really help keep you D.R.Y. by calling methods and data instead of building them everywhere they are needed.

5. Creating a Data Service

    Any time a service is made, it must be imported, added to the component provider array and declared inside the constructor, then anything in that service is accessible via this.ServiceDeclaration._____

    Raw data and methods can be stored in Data Services, then injected and called in other components.

    setting a property = this.service.property inside an ngOnInit method will grab the value from a service for use in that component.

6. Understanding the Hierarchical Injector

    if we provide a service in one component, the Angular framework knows how to create an angular framework for this component, and all of it's child components will receive the same instance of this service.

    Hierarchical Injector:

    AppModule: Same instance of Service is available Application Wide

    AppComponent: Same Instance of Servcie is available for all Components(but not for other Services)

    Any other Component: Same Instance of Service is available for the Component and all its child components.


7. How many Instances of Service Should It be?

    If a service is injected in a component, it also exists in all the child components. That means that if the service is provided in a component, it is a seperate instantiation of that service. If you want to access the service instance of the parent component, simply remove that service from the providers array. The service still needs to be injected to be called however.

8. Injecting Services into Services

    to inject a service into a service, it cannot be done on a component level, it must be 'provided' in the app module, in the providers array.

    Injection requires meta-Data to work, and services do not have meta-data. it must be placed in an @Injectable(){}.

    @Injectable is only required in services that have other services injected inside them. It is not required for services that get injected. However it may be required in future versions of Angular, and it is good practice for potential future-proofing.

9.  Using Services for Cross-Component Communication

    without services in order to do cross component we would need to build complex output/input chains.
    
    If services are injected into services, ensure the service is provided on the app module level

    add @injectable to a service where you want to inject it.

10. Services in Angular 6+
    If you're using Angular 6+ (check your package.json to find out), you can provide application-wide services in a different way.

    Instead of adding a service class to the providers[] array in AppModule , you can set the following config in @Injectable() :

        @Injectable({providedIn: 'root'})
        export class MyService { ... }

    This is exactly the same as:

        export class MyService { ... }
    and

        import { MyService } from './path/to/my.service';
        @NgModule({
       ...
        providers: [MyService]
        })
        export class AppModule { ... }
    Using this new syntax is completely optional, the traditional syntax (using providers[] ) will still work. The "new syntax" does offer one advantage though: Services can be loaded lazily by Angular (behind the scenes) and redundant code can be removed automatically. This can lead to a better performance and loading speed - though this really only kicks in for bigger services and apps in general.