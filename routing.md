1. Introduction:
   Angular ships with it's own router, making a single page seem like it reloaded, but it was Angular, the whole time!
2. Setting up and Loading Routes:
   In the app.module.ts create a route with
        const appRoutes: Routes = [
            { path: '', 
            component: HomeComponent
            } 
            { path: 'users', 
            component: UsersComponent
            } 
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
4. Styling Active Router Links
   angular has a built in directive to make router links dynamic
   in the <li> add routerLinkActive="active"
   to 
5. 
   