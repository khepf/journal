## What is an Observable? RxJS
- An observable is a data source (user input, events, http requests, triggered in code, etc)
- Observables are constructs to which you subscribe to be informed about changes in data
- For Observables provided by Angular, Angular unsubscribes for you. All others must be unsubscribed from (see below)
- Emitting new data is arguably the most important thing Observables do

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
      if (count === 2) {
        observer.complete();
      }
      
      if (count > 3) {
        observer.error(new Error('Count is greater than 3'));
      }
      count++;
    }, 1000)
  });
  
  this.firstObsSubscription = customIntervalObservable.subscribe(data => {
    console.log(data);
  }, error => {
    console.log(error);
    alert(error.message);
    // completion handler function
  }, () => {
    console.log('Completed');
  });
 }
```
#### Operators
- Data points reach these Operators that do something to the data, and then you subscribe to the result of these Operators
- Every observable has a pipe method. The pipe method is built into rxjs.
- You can chain as many operators as you want to the same pipe, one after another
- They allow you to build a chain of steps you want to funnel your observable data through
- learnrxjs.io/operators/

```
import { map, filter } from 'rxjs/operators';

this.firstObsSubscription = customIntervalObservable.pipe(filter(data => {
  return data > 0;
}), map((data: number) => {
  return 'Round ' + (data + 1);
})).subscribe(data => {
    console.log(data);
  }, error => {
    console.log(error);
    alert(error.message);
    // completion handler function
  }, () => {
    console.log('Completed');
  });
 }
 ```
 #### Subjects
