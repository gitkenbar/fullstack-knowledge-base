1. Introduction


2. Splitting Apps into Components
    Splitting components up is good for re-usability in larger apps. It also creates leaner components that are easier to comprehend.



3. Property & Event Binding Overview
   We can use Property and Event Binding in:
    Html Elements with Native Properties and Events
    Directives with Custom Properties and Events
        with ngStyle property binding
    Components with Custom Properties and Events


4. Binding to Custom Properties
    comment out problematic code until you're ready to handle it.

    by default all properties of components are only accessible from inside the component

    if you want a parent component to child property, you need to add a decorator

    format:

    @Input() property
    
    ex. property is an object

    @Input() element: {type: string, name: string, content: string}

    then the @selector needs to be imported from @angular/core

    Now any element that calls the component can call the new custom property


5. Assigning an Alias to Custom Properties

    Sometimes you want a property to have a different name if used in another componenet. You can set an Alias by passing it as a string in your property's argument

    format:

    @Input('Property Alias') Property

6. Binding to Custom Events

    you can pass ($event) as the argument when calling properties
    to make properties into events, we need to assign a "new EventEmitter" type

    A Decorator is required to access these Events outside of their component

    format:

    @Output() property = new EventEmitter<>

    Don't forget to import the decorator from '@angular/core'

    @Input() is for passing something "in"to the compenent

    @Output() is for passing something "Out" of the component

7. Assigning an Alias to Custom Events
    you can pass in a ('string') as an argument to an @Output() to change it's alias outside of the component

8. Custom Property and Event Binding summary

    Inputs and Outputs work fine for small use-cases,
    but things with greater scope would be impractical to chain imports and exports. In those cases services should be used.

9.  Understanding View Encapsulation

    Angular uses custom attributes to apply styles in different components, that is how it separates the styles of each of the component pieces.

    It emulates a "shadow-DOM" which is not supported by all browsers.

10. More on View Encapsulation
    
    @component decorator can have an encapsulation property set to ViewEncapsulation, which must be imported from '@angular/core'
    adding this property makes any styling done in this component Globally scoped
    
    you can add .none, .ShadowDom or .Emulated to the ViewEncapsulation imported from @Angular/core, which disables, uses ShadowDom or emulates ShadowDom, respectively.

    .emulated is the default


11. Using Local References in Templates

    local references are denoted with a #, this will hold reference to entire HTML element, not just the value. This reference is scoped to the component, and is only accessible inside of the component.

    Similar to an id, local references can be used to select HTML elements. As it grabs an entire element, the value must be read with #reference.value

12. Getting Access to the Template & DOM with @ViewChild

    Format--

    @ViewChild('selector', {static:true}) Property;

    Use string Interpolation and propertybinding if you want to output something on the DOM

    (add { static: true } as a second argument) needs to be applied to ALL usages of @ViewChild() (and also @ContentChild(), in section 17 below) IF you plan on accessing the selected element inside of ngOnInit().

    If you DON'T access the selected element in ngOnInit (but anywhere else in your component), set static: false instead!

    For projects using Angular 9 or higher (check the package.json file to find out), you can omit static: false, you only need to specify static: true if you plan on using the selected element inside of ngOnInit().

13. Projecting Content Into Components with ng-content

    everything you place between the opening and closing tag of your component is lost by default.

    there is a special directive called ng-content that uses an element selector <ng-content></ng-content> that can be used as a hook to mark the spot where the content in between component tags should be rendered.

    this is especially useful if you built a tab widget where each tab contains content from another HTML and property binding isn't appropriate. It also prevents cross-site scripting attacks.

14. Understanding the Component Lifecycle

    What is ngOnInit()?

    ngOnInit() is a life-cycle hook.

    when a new component is instantiated, it has multiple phases.

    ngOnChanges(): Called after a bound Input() property changes
        is executed when a new component is created, and whenever an Input() value changes.

        could be useful to store data before it is over-written or dumped
    ngOnInit(): Called once the component is initialized
        runs as soon as component is initialized, before it is rendered, it runs after the constructor()
    ngDoCheck(): Called during every change detection run
        runs any time change detection does a check, whether on button click, timer fired or observable resolution, 
        i.e. 
        ALL THE TIME
        this could be used to manually inform Angular about a change it wouldn't otherwise detect (very advanced Use-Case)
    ngAfterContentInit(): 
    Called after content (ng-content) has been projected into view
        called whenver content from ng-content has been initialized
    ngAfterContentChecked(): 
        Called every time the projected content has been checked
        executed after change detection checks the content projected onto the component

    ngAfterViewInit():
         Called after the component’s view (and child views) has been initialized
        executed once the view of the current component has been loaded
    ngAfterViewChecked():Called every time the view (and child views) have been checked
        this is called after all the changes are made, or if no changes are found
    ngOnDestroy(): Called once the component is about to be destroyed
        clean up, last chance to use object before it goes bye-bye

15. Seeing Lifecycle Hooks in Action



16. Lifecycle Hooks and Template Access

  You need to make sure that the data you are trying to access is available at the stage in the Lifecycle. if you try to access .textContent OnInit() you will get no result, however if you access .textContent AfterViewInit() it will be available

17. Getting Access to ng-content with @ContentChild

  @ContentChild is how we access what is in an <ngContent></ngContent> decorator
    like @ViewChild
    @ContentChild must be imported from '@angular/core'

    then the
    @ContentChild gets a selector, and a static property passed as an argument

    @ContentChild('selector', {static: true})

    then a property can be declared.



18. Wrap Up

    In this segment we Learned how to use Data Binding with Custom Properties and events, how to pass data around, how to access