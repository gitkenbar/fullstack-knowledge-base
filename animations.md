1. Module Introduction
    

    Angular ships with it's own animation system that can handle the adding of items to a list or conditional attaching and detaching of elements from the DOM, which would be difficult for regular CSS to handle.

2. Setting Up A Starting Project

With the release of Angular 4, the general syntax of Angular Animations didn't change. 

    However, the animation functions were moved into their own package and you now also need to add a special module to your imports[] array in the AppModule.

    Specifically, the following adjustments are required:

    You probably need to install the new animations package (running the command never hurts): npm install --save @angular/animations 
    Add the BrowserAnimationsModule to your imports[] array in AppModule
    This Module needs to be imported from @angular/platform-browser/animations' => import { BrowserAnimationsModule } from '@angular/platform-browser/animations' (in the AppModule!)
    You then import trigger , state , style etc from @angular/animations instead of @angular/core 


3. Animations Triggers and State

    Animations need to be declared in the component meta-data object as apart of the animations trigger() array. 
    the value is a trigger() and the argument passed should be a string that names the trigger, and an array which will contain state() methods. 
    In those state() you pass in the name of each state as a string, or a number, and a style method which contains an object that takes CSS code (dashes must be a 'string', otherwise use camelCase).
    
    trigger, state, and style must be imported from '@angular/core'

    an example of format:

@Component({
    selector: 'app-root',
    animations: [
    trigger('divstate', [
      state('normal', style({
        backgroundColor: 'red',
        transform: 'translateX(0)'
      })),
      state('highlighted', style({
        backgroundColor: 'blue',
        transform: 'translateX(100)'
      })),
      transition('normal => highleted', animate(300)),
      transition('highlighted => normal', animate(500))
    ])
  ]
})

and implementation looks like:
    <div [@divstate="state"]></div>

4. Switching between States

    Animation states can be changed just like any other property, such as through an event listener and a method.

    An example method:

    onAnimate() {
      this.state == 'normal' ? this.state = 'highlighted' : this.state = 'normal'
    }

5. Transitions

    transition(), which must be imported from '@angular/core', as a first argument expects a starting state then an arrow => finished state, then animate(transition speed in ms) which must also be imported from '@angular/core'

6. Advanced Transitions

    for transitions that are the same speed the transition string arrow can be pointed both directions <=>

    * is a wildcard transition, meaning it doesn't matter which state of the animation it is currently in, it will switch. Especially useful if the state is created dynamically, and we have no idea where it might be transitioning from.

7. Transition Phases

    the animate() function can do more than control the timing, it can also pass styles and control the entire animation.

    in order to create animation phases, an array can be used as the second transition() argument.

    if you set the style() in the array, it instantly changes, or if you use an animate() the transition speed can be set as the first argument, and the second argument can be a style function

8. The "void" State

    if animating an element being added to or removed from the dom, the void state is the starting state. void is a reseved name, you cannot use it.

    if adding components dynamically with *ngIf the animation binding goes in the same element and doesn't need to be bound to the starting state, because the starting state is void.
    
    if transitioning in to the DOM the void => can be set to wildcard * i.e.

        transition('void => *', animate(300))


9.  Using Keyframes for Animations

    using the keyframes() as a second argument in an animate() allows greater control over the way the animation renders.

    by default styles in the keyframe array are displayed an equal amount of time, this can be overwritten by passing the offset: 0-1 property.

10. Grouping Transitions

    the group() method, which must be imported from '@angular/core', can be used to group two seperate animations so that they can run simultaneously but not synchronously.

11. Using Animation Callbacks

    there are built in event listeners to animations, like .start and .done that can be used to trigger functions.

    it is formatted like:

    (@animationName.start)="methodName(argument)"