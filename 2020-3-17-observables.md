## What is an Observable? RxJS
- An observable is a data source (user input, events, http requests, triggered in code, etc)
- Observables are constructs to which you subscribe to be informed about changes in data
- For Observables provided by Angular, Angular unsubscribes for you. All others must be unsubscribed from (see below)

- An Observer is your code (subscribe, etc)

#### Three ways to handle data packages
1. Handle Data
2. Handle Error
3. Handle Completion of the observable

```
this.route.params.subscribe( next: (params: Params) => {
  this.id = +params.id;
 });
}
```
```
import { interval, Subscription } from 'rxjs;

private firstObsSubscription: Subscription;

someMethod() {
  this.firstObsSubscription = interval(1000).subscribe(count => {
    console.log(count);
  })
 }
 
 ngOnDestroy(): void {
  this.firstObsSubscription.unsubscribe();
 }
 ```
 #### Building a custom observable
 ```
 import { Observable } from 'rxjs';
 
 private firstObsSubscription: Subscription;
 
 someMethod() {
  const customIntervalObservable = Observable.create((observer) => {
  let count = 0;
    setInterval(() => {
      observer.next(count);
      count++;
    }, 1000)
  });
  
  this.firstObsSubscription = customIntervalObservable.subscribe(data => {
    console.log(data);
  });
 }
