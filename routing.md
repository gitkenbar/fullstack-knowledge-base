1. Introduction:
   Angular ships with it's own router, making a single page seem like it reloaded, but it was a singular Angular, the whole time!

2. Setting up and Loading Routes:
   In the app.module.ts create a route with
        const appRoutes: Routes = [
            { path: '', 
            component: HomeComponent
            } ,
            { path: 'users', 
            component: UsersComponent
            } ,
            { path: 'servers', 
            component: ServersComponent
            } 
        ]

    also importing routes from @angular/router with
        import { Routes } from '@angular/router';
    isn't required, but is 'good practice'

    add the RouterModule to the imports array in the @NgModule with the .forRoot(appRoutes) passing in the Routes const

3. Navigation with Router Links
   href reloads page on default. Angular includes routerLink="/" 
   event binding works too [routerLink]="['/users']"

   relative paths are usable in the root module, but won't work in a component. navigation is possible in router links i.e. "../servers"
4. Understanding Navigation Paths



5. Styling Active Router Links
   angular has a built in directive to make router links dynamic
   in the <li> add routerLinkActive="active"
   to 

6. Navigating Programmatically


6. Using Relative Paths in Programmatic Navigation


7. Passing Parameters to Routes

   it would be nice if we could pass the id of a user to a route path.
   adding : before the property indicates that the path is dynamic 
   {path: 'users/:id/:name', component UserComponent}

   referenced with string interpolation {{ property}}

8. Fetching Route Parameters

   How do we access the data in the URL?
   we inject the ActivatedRoute in the .ts to get access to the currently loaded route.
   the route data is stored as a .js object with lots of meta-data about the loaded route.

   implement OnInit, and set the this.property = 
   {id: this.route.snapshot.params['property'],
   name: this.route.snapshot.params['property']}


9.  Fetching Route Parameters Reactively

   router links can be customized with a structure of 'route', 'id', 'name'
   [routerLink]="['/users', id, 'anna']"
   putting this inside the dynamic route will cause a bug, not reloading the component with updated data. this is angular working as intended. as the link keeps the user on the same active component, just updates the data.

   because the snapshot.params is initialized OnInit it only updates when the component is loaded for the first time. If we are trying to update the data in the URL.

   This can be avoided by using an observable in the OnInit function:
      this.route.params.subscribe(
         (params: Params) => {
            this.user.id = params['id'];
            this.user.name = params['name'];
         }
      );

   using an observable instead of a snapshot is not required. It simply increases functionality if the route is changed within the component

10. An Important Note about Route Observables


12. Passing Query Parameters and Fragments


13. Retrieving Query Parameters and Fragments
   