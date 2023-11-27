1. Intro


2. How an Angular App gets Loaded and Started


3. Components are Important


4. Creating a New Component


5. Understanding the Role of AppModule and Component Declaration


6. Using Custom Components


7. Creating Components with the CLI & Nesting Components


8. Working with Component Templates
 you can use an in-line template, where you use HTML in the template in the servers component.
    every component needs a template, it is required
    backticks can be used to write multi-line templates.
1. Working with Componenet Styles
    styleURLs: [] is an array, and can include many css files.
    you can also add Styles:[] and write CSS in-line
    you cannot, however do both, once you pick one, stick with it.
2.  Fully Understanding the Component Selector
    Your selector needs to be Unique, it cannot be mistaken for another selector, or a selector provided by a third party package.
    selectors work like css selectors, so you are not limited to selecting elements.
    you can enclose your selector in [] to make it an Attribute to include it in a <div selector>
    selectors can also be classes by inputting
    selector: '.app-servers' and calling it in a class, i.e. div.app-servers or <div class="app-servers">
3.  What is Databinding?
    communication between typescript code and the template. Typescript is backend data retrieval and manipulation and the template is what the user sees.
    .ts code ---- Output Data ---> template (.html)
    we can use String Interpolation - {{ data }}
    Property Binding - [property]="data"
    .ts code <--- react to user events ---- template.html
    Event Binding (event)="expression"

    Combination of Both: Two-Way-Binding ->[(ngModel)]="data"

4.  String Interpolation
    Format -- {{ typescript expression }} example is would be a property, or a hard-coded string, or a method that returns a string. You cannot do a block expression, but you can use a ternary expression. 
    numbers are usable, as they can easily be converted to strings

5.  Property Binding
    Square brackets [] indicate to angular that we want to bind to a property.
    each HTML element can be bound
    syntax : [property]="data of the type property specifies"
    
6.  Property Binding vs String Interpolation
    if you want to output data in your template, print some text to it, use string interpolation.

    if you want to change a property, of an HTML element, directive or component.

    string interpolation only works in a normal template, not within another expression of that template

7.  Event Binding
    logic can go inside the quotation marks, such as changing a boolean value, but anything more complex would be bad practice.
    typically you have onclick method, but in angular we use event binding
    format - (event)="method()"

8.  Passing and Using Data with Event Binding
    $event is a reserved word that gives us access to event data
    (<HTMLInputElement>event.target).value
    using () indicates that we know that the type of the HTML element of this event will be an HTML input element, we do explicit casting with (<type>)
9.  Two-Way-Databinding
    form- [( data )]

    two way binding is a good way to reacting to changes in a value, even when the value is changed in another place


    Important: For Two-Way-Binding (covered in this lecture) to work, you need to enable the ngModel directive. This is done by adding the FormsModule to the imports[] array in the AppModule.

    You then also need to add the import from @angular/forms in the app.module.ts file:

        import { FormsModule } from '@angular/forms';

    To be able to use 'ngModel', the FormsModule (from @angular/forms) needs to be added to your imports[] array in the AppModule  (should be there by default in a CLI project)!


18. Combining all Forms of Databinding

19. Understanding Directives
    
    @Directive ({
        selector : '[ ]'
    })
    export class 

    components are directives with a template
    there are also directives without templates

    directives can be configured like the selector of a component

20. Using nglf to Output Data Conditionally
    the asterisk in *ngIf indicates that it is a structural directive
    
    ngIf adds and removes it from the DOM it doesn't hide it, it simply isn't there

    *ngIf="any method that returns a boolean"
21. Enhancing nglf with an Else Condition
    <ng-template #>
    # is indicative of a local reference, think of it as a marker
22. Styling Elements Dynamically with ngStyle
    
    unlike structural directives, attribute directives don't add or remove elements, just change the element they are placed on
    ngStyle does not get an *asterisk*
    [ngStyle] the [] indicates we want to bind onto this property of the directive, the [] is not part of the directive

23. Applying CSS Classes Dynamically with 
    
    ngClass allows us to dynamically add and remove CSS classes

    [ngClass]="{}"
    
24. Outputting Lists with ngFor
    
    *ngFor="let server of servers" will loop through the server items of the servers array, much like a for/of loop.

25. Getting the Index when using ngFor
    

    








 27. working with Component Templates
    
27. working with component styles
