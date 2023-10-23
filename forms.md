1. Introduction to Forms
   In a single Page app there is no "submitting to server"
   You will have to use Angular's HTTP service.
    Angular will let you check if a form is valid, it will allow you to change conditions, like changing the format for an invalid entry.
2. Why do we need Angular's Help?
   The form itself is basic HTML code, but the data handling will be JS or more specifically TypeScript.
   In TypeScript we can define the value, and we can also define meta-data, like if the user input is valid.
   
   We can store the value as an object. where the inputs specified in the form can be the key of a key-value pair, and the value is the user input.

3. Template Driven (TD) vs Reactive Approach
   
    Template-Driven: Angular Infers the Form Object from the DOM
            Easier to get started quickly


    Reactive Approach: Form is created programmatically and sychronized with the DOM.
            Here you manually define the structure of the Typescript code, set up the HTML code, and manually connect it to the HTML. Which may sound more complicated than it is, it does allow more customization.

4. an Example Form
   
   In the form tag, there is no action attribute pointing to a route, nor specifying the method, either. That is because there is no HTTP request, Angular handles it all.

5. TD: Creating the Form and Registering the Controls
   
    Angular automatically creates a Javascript representation of the form when it detects a form element in HTML.
    You can think of the <form> element serving as a selector for an angular directive, which creates the JavaScript representation.
    It would be very empty, though. Angular could find the inputs, but it doesn't want to assume an input is relevant to the form. Maybe there's inputs that change the UI of the form, and isn't relevant form data. Or perhaps you have a custom or third party input that Angular wouldn't recognize as form data.

    All input controls need to be registered manually. in Template Driven, it's really simple. adding: 
        ngModel name="value" 
    lets angular know that an input is a control, where "value" is the name of the control.
    

6. TD: Submitting and Using the Form
   a button of type="submit" will generate a submit event that's built into HTML and Javascript. Angular gives us a directive to place on the form element called (ngSubmit) that only gives us one event to listen to.

    In template driven forms, everything will be done in the template.

    if you wanted to test the form you could add a local reference '#f' and pass that reference as an argument in the function called in the (ngSubmit)="function(f)"
    then in the typescript, format the function to accept as an argument (form: HTMLFormElement), then you can console.log(form);

    The default way to get access to the automatically generated object. is to add ="ngForm" to a #localReference. Ex:
    #form="ngForm"

    remember that the form element is a selector for a built-in Angular directive that builds the javascript object automatically, and will expose data that can be fetched on the form element.

    NgForm can be set as the type of a form argument, but must be imported from '@angular/forms'

    when you log the form: NgForm you get an NgForm object which has a lot of properties we did not create. It does however have a value property, which when expanded, shows us the key value pairs that have the names of the inputs we have selected.

7. TD: Understanding Form State
   
   the controls property contains all the form controls that are registered to angular. they each have properties similar to the properties of NgForm, like dirty, disabled, submitted etc.

   dirty: true; property has been changed
   valid: true; property is valid, or has been validated (i.e. email address format checker)
    touched: true; property has been interacted with

8. TD: Accessing the Form with @ViewChild
   
    @ViewChild allows us to access a local reference in our typescript code. #f="ngForm" is just such a local reference.
    we can pass the local reference as an argument in @ViewChild in the AppComponent, then assign a property to it. format example:

    @ViewChild('f') signupForm: NgForm;

    onSubmit() {
        console.log(this.signupForm)
    }

9.  TD: Adding Validation to check User Input
    
    without validation, a form can be submitted with any kind of input, or even no input at all. Validation should of course be done by the server, but we can also do some validation on the front end, like ensuring required fields are filled in, or an email address follows the correct format.

    adding required acts as a selector for a built-in directive shipping wit hangular and it will automatically configure the form to treat it as invalid if it is empty.

    email is another directive made available by angular that determines if the input fits the format of an e-mail address. It not only tracks this on the form level but also on a per control basis.

    angular adds and removes classes to signify the state of the element, these classes can be used to style the form

10 Built-in Validators & Using HTML5 Validation

    Which Validators do ship with Angular?

    Check out the Validators class: https://angular.io/api/forms/Validators - these are all built-in validators, though that are the methods which actually get executed (and which you later can add when using the reactive approach).

    For the template-driven approach, you need the directives. You can find out their names, by searching for "validator" in the official docs: https://angular.io/api?type=directive - everything marked with "D" is a directive and can be added to your template.

    Additionally, you might also want to enable HTML5 validation (by default, Angular disables it). You can do so by adding the ngNativeValidate to a control in your template.

11. TD: Using the Form State

    using [disabled]="formReference.valid" will check if the form is valid and disable the button if the check comes back false. Format:
        [disabled]="!f.valid"

    styling the inputs needs to be explicit on it's targeting, which is pure css logic, otherwise the entire form and input groups will be styled, and will look horrible.

    example:
        input.ng-invalid{
             border: 1px solid red;
        }

    If we want a style to apply with multiple classes, such as ng-invalid and ng-touched, then they are added together like adding classes to a newly created element. format:
        .ng-invalid.ng-touched
    
12. TD: Outputting Validation Error Messages
    
    A quick way of getting access to the control created by Angular automatically is to add a #localReference.

    adding ="ngModel" directive to a local reference exposes additional information about the control it creates by accessing ngModel. such as whether or not it was touched or changed

    *ngIf="!email.valid && email.touched"


13. TD: Set Default Values with ngModel Property Binding
    
    you can use one-way property binding with [ngModel]="property" to set a default value. defining the property in the component.ts file in the component export class. this is over-writable.

14. TD:Using ngModel with Two-Way-Binding
    
    if you need a responsive change in your form you can use two way binding of ngModel with this format:
        [{ngModel}]="property"

    the user input will still be submitted with the submit button, but two way binding updates the property on every keystroke.

15. TD: Grouping Form Controls
    
    grouping forms is good to keep large forms organized.
    ngModelGroup is the built in directive to do so, it needs to be set equal to a string, that will be the label or key to the group.

    a local reference can be set equal to ngModelGroup to achieve the same end, and that reference can be used with *ngIf="" to check if .valid or .touched

16. TD: Handling Radio Buttons
    
    Radio buttons can be populated by defining an array and using *ngFor="let singular of plural" where singular is the name of each item in the array.
    ngModel can be set with property binding to define a default value
    of course the required directive can be used to require a selection

17. TD: Setting and Patching Form Values
    
    the .setValue() method can be used to change the values of every property within an object, but it isn't ideal in most circumstances.

    the patchValue({}) method can be used to only over-write specific controls, but in example given it had to be instantiated off of the .form instead of the signupForm.

18. TD: Using Form Data
    
    the data can be utilized by instantiating a user object with corresponding properties to the data collected. this user object can be populated with the data through an onSubmit() and can then be accessed using property binding? {{ property.key }}

19. TD: Resetting Forms
    
    resetting the form is super simple. just call .reset() after the property that holds the form, in the example case the syntax is:

    this.signupForm.reset()

    if you want you can pass the same object as in setValue() to reset() which will then reset the form to specific values!

20. Introduction to Reative Approach
    
21. Reactive: Setup
    
22. Reactive: Creating a Form in Code
    
23. Reactive: Syncing HTML and Form
    
24. Reactive: Submitting the Form
    
25. Reactive: Adding Validation
    
26. Reactive: Getting Access to Controls
    
27. Reactive: Grouping Controls
    
28. Reactive: Arrays of Form Controls (FormArray)
29. Reactive: Creating Custom Validators
30. Reactive: Using Error Codes
31. Reactive: Creating a Custom Async Validator
32. Reactive: Reacting to Status or Value Changes
33. Reactive: Setting and Patching Values