Understanding Observables
1. Introduction
   
   In our angular project, an observable is just an object we import from a third-party package RxJS
    observable pattern Observable -> observer
    the observable can have multiple events, or data packages emitted by the observable.

    Observer can:
    1. Handle Data 2. Handle Error 3. Handle Completion
    You, the developer, can control what the Observer does in each of these instances

    similar to call-backs and promises, observables are just a different way to approach them, and have potential advantages.


2. Analyzing Angular Observables
   

3. Getting Closer to the Core of Observables
   
   Observables are a feature that's not baked into JS or TS, but added by a package from RXJS.

    Observables don't stop emiting values(data) when you aren't looking at them.
    If you don't shut down the process it will grow into a memory leak, occupying limited user resources and slowing down the app

    For the observables provided by Angular, like params (but there are other examples), Angular takes care of unsubscriptions

4. Building a Custom Observable
   format--
    const customIntervalObservable = Observable.create(() => {})
    the Anonymous arrow function will get an argument automatically from RxJS. that argument is an Observer

    The Observer is the part that is interested in new Data, errors, or completion of the observer.

    then inside your arrow function you can pass in setInterval() with another arrow function inside of that. In this function you can pass arguments


5. Errors and Completion
   

6. Observables and You
   

7. Understanding Operators
   

8. Subjects
   

9.  Wrap Up