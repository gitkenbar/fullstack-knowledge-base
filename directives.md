1. Intro
   We will learn how to build our own directives
   We will learn what the * means in a directive.

   Attribute Directives:
    AD only change attributes and styling of elements
   Structural Directives:
    SD can change the DOM, create and destroy elements from the DOM
2. ngFor and ngIf Recap
    these are Structural Directives
    
    *ngFor="let number of numbers"
    instantiates a number for each item in the numbers array in the .ts file

    *ngIf="number % 2(modulus) == 0

    Only one structural directive is allowed on a single element, but you can put an element with a structural Directive inside a div with structural Directive

    later, we will learn how to use pipes to dynamically filter arrays

3. ngClass and ngStyle Recap
   
   the property binding around [ngClass] indicates we're binding to a property in the ngClass directive

    [ngClass]="{odd: odd % 2 !== 0}"
    odd css class only displays if odd divided by 2 isn't 0, or if it has a remainder,


    ngStyle allows us to pass an object to a property which is named ngStyle on the same directive.

    [ngStyle]="{backgroundColor: odd % 2 !== 0 ? 'yellow' : 'transparant'}"
    this uses a ternary operator, it checks if the property is odd, and if it is, it is 'yellow' if not, it is 'transparent'

4. Creating a Basic Attribute Directive
   
    A directive needs to have a descriptive export class

    A directive must import Directive from '@angular/core'

    to make it a directive we have to make it an @Directive() we need to pass an object to the directive to configure it.
        selector: the name used to call the directive, it should be descriptive and camelCased so it is easy to read
            a plain 'selector' would select by element
            '[selector]' would be recognized without square brackets in an element. such as:

    Angular allows an element the directive sits on to be injected into this directive, injection will be covered more in services module. a better way to get access to classes without instantiating them.


    adding 'private' to the constructor argument will make it a property of the class and automatically assign the value to the property

    Directives need to be declared in the app.module.ts in the @NgModule({declarations: [array]}) to be recognized by Angular

    changing element the directive sits on can be selected with:
            this.(property from the constructor).nativeElement
    styling is better done on ngOnInit than in the constructor itself

5. Using the Renderer to build a Better Attribute Directive
   
    the above method works but isn't 'good practice' because angular can render the templates without a DOM and these properties wouldn't be available.

    use:
        ng (g)enerate (d)irective directiveName
    to create a new directive using the CLI


    implement a constructor:
    constructor(private elRef: ElementRef, private property: Renderer2)
    ElementRef and Renderer2 MUST be imported from '@angular/core'


    initialization of directives is best done with ngOnInit() function, be sure to implement it in the export, and import it from '@angular/core'


    style can be changed using ngOnInit() 
    ngOnInit(){ 
        this.renderer.setStyle(elementSelector, Style, value, flags) 
        }

    you need to access nativeElement after the elementRef property, as the element reference cannot be passed by itself, the underlying element needs to be selected.

    Style refers to the style you want to change, i.e. 'background-color' it must be a string

    Value is the value of the changed style i.e. 'blue'

    flags are optional, they allow special attributes like 'important' that affect the way the renderer works.


    why is the renderer better?
        angular is not limited to the browser, it works with service workers. these might not have access to the DOM, if you tried to change the DOM you may get an error.
        


6. Using HostListener to Listen to Host Events

    @HostListener() can be used to make styling more dynamic.
    Host listener takes argument name as an input.
    all events available through event binding are passable as an argument.

    after the @HostListener(), a method then needs to be passed.
    a custom event can also be used. This event would have access to the event data, which is the property defined in the argument of the method

    @HostListener('mouseenter') mouseover(eventData: Event) {

    }

   
7. Using HostBindig to Bind to Host Properties
   
    the @HostBinding decorator needs to be bound to a property which value will become important, which could be backgroudColor: string;

    in @HostBinding a string can be passed defining which property of the hosting element we want to bind, i.e. 'style.backgroundColor' camelCase is important, as the DOM property doesn't know dashes.

    with Hostbinding, any property of the element referenced can be bound to

8. Binding to Directive Properties

    Hostbinding and HostListener are great for dynamic styling, but the user of the directive should be able to dynamically set the value. Maybe we want to change colors based on other parameters.

    First the properties to be bound need to be added with @Input decorator

    next, the property and therefore it's value can be called via this.propertyName in the HostListener

    now we can bind the default color with property binding:
        [defaultColor]="'yellow'"
    be sure to make the value a string by including '' in the ""



   
9.  What Happens behind the Scenes on Structural Directives
    
10. Building a Structural Directive
    
11. Understanding ngSwitch