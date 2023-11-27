1. Intro
    In this Module we will look at dynamic components. Dynamic components are components that we want to create on run-time.
    Ex:
    If we want to display a modal or overlay which should only be loaded upon a certain action(i.e an error message).

2. Adding an Alert Modal Component

    There's nothing wrong with in-line alerts and error messages, but dynamic modals are fancy AF.

    the backdrop is 'that thing in the background that blocks access to the rest of the page and the focus is on the alert box'

    in our alert component, we have a message property we want to output, therefore in the alert.component.ts we need to set the property of message: string; and be sure to add the @Input decorator

3. Understanding the Different Approaches

    Dynamic components should only be displayed if a certain part of the code is being used.

    Therefore any dynamic component needs to be loaded programatically:

    *ngIf: is awesome, allows declaritive approach. which means you simply add that component selector in your template then use *ngIf to only add it to the DOM under a certain condition. No Major downsides.

    Dynamic Component Loader: Component created and added to DOM via code(imperatively)
    Component is managed & added by develper
    
    developer manually controls how it's instantiated, that data is passed into it, also that it is removed.

    could be useful in certain use cases, but otherwise avoided entirely.

4. UsingngIf

    Using ngIf means we don't have to manually create it, we can easily pass data using property binding. It makes event listening simple and straightforeward.

    If we want to make sure we can get rid of the alert all we need to do is emit an event.

    Closing alert modals can be done by creating an @Output() event emitter, a method that manually emits that event emitter, add an event listener in the app selector element with *ngIf that listens to the emitted event, and runs another method that resets this.error by setting this.error = null

5. Preparing Programmatic Creation

    import ComponentFactoryResolver from @angular/core, inject it in the constructor
    this gives access to this.componentFactoryResolver.resolveComponentFactory(component).
    if you set a property to this, it will return a component factory, not the component itself.

    we still need to define where this component will be constructed with a view container ref (an object managed internally by Angular which gives Angular a reference) 

    for this we can create a helper directive:
    
    --placeholder.directive.ts----

    import { Directive } from '@angular/core';

    @Directive({
        selector: '[]'
    })

    export class Placeholder Directive {}

    
    

6. Creating a Component Programmatically


7. Understanding entryComponents


8. Data Binding & Event Binding


9.  Wrap Up


10. Links

