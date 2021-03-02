# Provide the Service

You must make the `HeroService` available to the dependency injection system before Angular can *inject* it into the `HeroesComponent` by registering a *provider*. A provider is something that can create or deliver a service; in this case, it instantiates the `HeroService` class to provide the service.

To make sure that the `HeroService` can provide this service, register it with the *injector*, which is the object that is responsible for choosing and injecting the provider where the app requires it.

By default, the Angular CLI command `ng generate service` registers a provider with the *root injector* for your service by including provider metadata, that is `providedIn: 'root'` in the `@Injectable()` decorator.

```typescript

      @Injectable({  providedIn: 'root', })    
```

When you provide the service at the root level, Angular creates a single, shared instance of `HeroService` and injects into any class that asks for it. Registering the provider in the `@Injectable` metadata also allows Angular to optimize an app by removing the service if it turns out not to be used after all.

# HttpClient 

All `HttpClient` methods return an RxJS `Observable` of something.

HTTP is a request/response protocol. You make a request, it returns a single response.

In general, an observable *can* return multiple values over time. An observable from `HttpClient` always emits a single value and then completes, never to emit again.

This particular `HttpClient.get()` call returns an `Observable<Hero[]>`; that is, "*an observable of hero arrays*". In practice, it will only return a single hero array.

### `HttpClient.get()` returns response data

`HttpClient.get()` returns the body of the response as an untyped JSON object by default. Applying the optional type specifier, `<Hero[]>` , adds TypeScript capabilities, which reduce errors during compile time.

The server's data API determines the shape of the JSON data. The *Tour of Heroes* data API returns the hero data as an array.



# Observable

Observables are lazy collections of multiple values over time.

1. **Observables are lazy**
   You could think of lazy observables as newsletters. For each subscriber a  new newsletter is created. They are then only send to those people, and  not to anyone else.

2. **Observables can have multiple values over time**
   Now if you keep that subscription to the newsletter open, you will get a  new one every once and a while. The sender decides when you get it but  all you have to do is just wait until it comes straight into your inbox.

3.  **Observables are cancelable.** 

    If you don’t want your newsletter anymore, you unsubscribe. With  **promises** this is different, you can’t cancel a promise. If the promise  is handed to you, the process that will produce that promise’s  resolution is already underway, and you generally don’t have access to  prevent that promise’s resolution from executing.



**Pull**

When pulling, the data consumer  decides when it get’s data from the data producer. The producer is  unaware of when data will be delivered to the consumer.

**Push**

Promises are the most common way of push in JavaScript today. A promise (the  producer) delivers a resolved value to registered callbacks (the  consumers), but unlike functions, it is the promise which is in charge  of determining precisely when that value is “pushed” to the callbacks.

Observables are a new way of pushing data in JavaScript. An observable is a  Producer of multiple values, “pushing” them to subscribers.

## Creating an observable yourself

```javascript
import { Observable } from "rxjs/Observable"

// create observable
const simpleObservable = new Observable((observer) => {
    
    // observable execution
    observer.next("bla bla bla")
    observer.complete()
})

// subscribe to the observable
simpleObservable.subscribe()

// dispose the observable
simpleObservable.unsubscribe()
```

**Subscribing to observables
**Remember,  observables are lazy. If you don’t subscribe nothing is going to happen. It’s good to know that when you subscribe to an observer, each call of `subscribe()` will trigger it’s own independent execution for that given observer.

On the parameter that was given when creating the observable there are  three functions available to send data to the subscribers of the  observable:

- “next”: sends any value such as Numbers, Arrays or objects to it’s subscribers.
- “error”: sends a Javascript error or exception
- “complete”: does not send any value.

Calls of the next are the most common as they actually deliver the data  to it’s subscribers. During observable execution there can be an  infinite calls to the `observer.next()`, however when `observer.error()` or `observer.complete()` is called, the execution stops and no more data will be delivered to the subscribers.

**Disposing observables
**Because observable execution can run for an infinite amount of time, we need a  way to stop it from executing. Since each execution is run for every  subscriber it’s important to not keep subscriptions open for subscribers that don’t need data anymore, as that would mean a waste of memory and  computing power.

When you subscribe to an observable, you get back a subscription, which represents the ongoing execution. Just call `unsubscribe()`to cancel the execution.

# Subjects

A Subject is like an Observable. It can be subscribed to, just like you normally would with Observables. It also has methods like `next()`, `error()` and `complete()` just like the observer you normally pass to your Observable creation function.

The main reason to use Subjects is to multicast. An Observable by default  is unicast. Unicasting means that each subscribed observer owns an  independent execution of the Observable. To demonstrate this:

```javascript
import * as Rx from "rxjs";

const observable = Rx.Observable.create((observer) => {
    observer.next(Math.random());
});

// subscription 1
observable.subscribe((data) => {
  console.log(data); // 0.24957144215097515 (random number)
});

// subscription 2
observable.subscribe((data) => {
   console.log(data); // 0.004617340049055896 (random number)
});
```

Multicasting basically means that one Observable execution is shared among multiple subscribers.

Subjects are like EventEmitters, they maintain a registry of many listeners. When calling subscribe on a Subject it does not invoke a new execution  that delivers data. It simply registers the given Observer in a list of  Observers

Whereas Observables are solely data producers, Subjects can both be used as a  data producer and a data consumer. By using Subjects as a data consumer  you can use them to convert Observables from unicast to multicast.  Here’s a demonstration of that:

```typescript
import * as Rx from "rxjs";

const observable = Rx.Observable.create((observer) => {
    observer.next(Math.random());
});

const subject = new Rx.Subject();

// subscriber 1
subject.subscribe((data) => {
    console.log(data); // 0.24957144215097515 (random number)
});

// subscriber 2
subject.subscribe((data) => {
    console.log(data); // 0.24957144215097515 (random number)
});

observable.subscribe(subject);
```



# The BehaviorSubject

https://medium.com/@luukgruijs/understanding-rxjs-behaviorsubject-replaysubject-and-asyncsubject-8cc061f1cfc0

The BehaviorSubject has the characteristic that it stores the “current”  value. This means that you can always directly get the last emitted  value from the BehaviorSubject.

```typescript
import * as Rx from "rxjs";

const subject = new Rx.BehaviorSubject();

// subscriber 1
subject.subscribe((data) => {
    console.log('Subscriber A:', data);
});

subject.next(Math.random());
subject.next(Math.random());

// subscriber 2
subject.subscribe((data) => {
    console.log('Subscriber B:', data);
});

subject.next(Math.random());

console.log(subject.value)

// output
// Subscriber A: 0.24957144215097515
// Subscriber A: 0.8751123892486292
// Subscriber B: 0.8751123892486292
// Subscriber A: 0.1901322109907977
// Subscriber B: 0.1901322109907977
// 0.1901322109907977
```

There are a few things happening here:

1. We first create a subject and subscribe to that with Subscriber A. The  Subject then emits it’s value and Subscriber A will log the random  number.
2. The subject emits it’s next value. Subscriber A will log this again
3. Subscriber B starts with subscribing to the subject. Since the subject is a  BehaviorSubject the new subscriber will automatically receive the last  stored value and log this.
4. The subject emits a new value again. Now both subscribers will receive the values and log them.
5. Last we log the current Subjects value by simply accessing the `.value` property. This is quite nice as it’s synchronous. You don’t have to call subscribe to get the value.

Last but not least, you can create BehaviorSubjects with a start value.  When creating Observables this can be quite hard. With BehaviorSubjects  this is as easy as passing along an initial value. See the example  below:

```typescript
import * as Rx from "rxjs";

const subject = new Rx.BehaviorSubject(Math.random());

// subscriber 1
subject.subscribe((data) => {
    console.log('Subscriber A:', data);
});

// output
// Subscriber A: 0.24957144215097515
```

# Pipes

“A pipe is a way to write display-value transformations that you can  declare in your HTML. It takes in data as input and transforms it to a  desired output”.

https://itnext.io/understanding-angular-pipes-5d1154f57d4f

# Routing

links:

https://medium.com/angular-in-depth/the-three-pillars-of-angular-routing-angular-router-series-introduction-fb34e4e8758e

The core focus of the router is to enable navigation among routable  components within an Angular application, which requires the router to **render a set of components using an outlet on the page, and then reflect the rendered state in the url.** In order to do this, the router needs some way to associate urls with the  appropriate set of components to load. It accomplishes this by letting a developer define a router state configuration object, which describes  which components to display for a given url.

```javascript
import { RouterModule, Route } from '@angular/router';

const ROUTES: Route[] = [
  { path: 'home', component: HomeComponent },
  { path: 'notes',
    children: [
      { path: '', component: NotesComponent },
      { path: ':id', component: NoteComponent }
    ]
  },
];

@NgModule({
  imports: [
    RouterModule.forRoot(ROUTES)
  ]
})
```

It will produce the following tree of router states when passed into `routerModule.forRoot()` :

<img src="https://miro.medium.com/max/1386/1*_ySB8CTLi45dBvUj8Sqxgg.png" alt="Image for post" style="zoom: 50%;" />

An important point is that at any time, some router state (i.e.  arrangement of components) is being displayed on screen to the user,  based on the current url. This arrangement is known as the active route. **An active route is just some subtree of the tree of all router states**. For instance, the url `/notes` would be represented as the following active route:

<img src="https://miro.medium.com/max/1366/1*WBnoxr-Hd6LacI4mltwcFg.png" alt="Image for post" style="zoom:50%;" />

1. The RouterModule has a `forChild` method, which also accepts an array of Routes. While both `forChild` and `forRoot` return modules containing all of the router directives and route configurations, `forRoot` also creates an instance of the Router service. [**Since  the Router service mutates the browser location, which is a shared  global resource, there can be only one active Router service**.](https://blog.angularindepth.com/avoiding-common-confusions-with-modules-in-angular-ada070e6891f) This is why you should use `forRoot` only once in your application, in the root app module. Feature modules should use `forChild`.

2. When a route’s path is matched, the components referenced inside of the router state’s `component` properties are rendered using router-[*outlets*](https://angular.io/api/router/RouterOutlet)*,* which are dynamic elements that display an activated component. Technically, the components will be rendered as a *sibling* to the router outlet directive, not inside of it. Router outlets can  also be nested within one another, forming parent/child route  relationships.

At any given point in time, **the URL represents a serialized version of the application’s currently activated router state**. Changes in the router state will change the URL, and changes in the URL will change the router state. They are both representations of the same thing.

<img src="https://miro.medium.com/max/1380/1*PTDVdMLfL8nihVgm2X0NgQ.png" alt="Image for post" style="zoom:50%;" />

During this **navigation cycle, the router emits a series of events**. The Router service provides an observable for listening to router  events, which can be used to define logic, such as running a loading  animation, as well as aiding in debugging routing. Some noteworthy  events during this cycle are:

`NavigationStart:` Represents the start of a navigation cycle.

 `NavigationCancel:` For instance, a guard refuses to navigate to a route. 

`RoutesRecognized:` When a url has been matched to a route. 

NavigationEnd: Triggered when navigation ends successfully.

# RxJS The map operator

https://medium.com/@luukgruijs/understanding-rxjs-map-mergemap-switchmap-and-concatmap-833fc1fb09ff

The map operator is the most common of all. For each value that the Observable emits you can apply a function  in which you can modify the data. The return value will, behind the  scenes, be reemitted as an Observable again so you can keep using it in  your stream. It works pretty much the same as how you would use it with  Arrays. The difference is that Arrays will always be just Arrays and  while mapping you get the value of the current index in the Array. With  Observables the type of data can be of all sorts of types. This means  that you might have to do some additional operations in side your  Observable map function to get the desired result. Let’s look at some  examples:

import { of } from 'rxjs'; 

import { map } from 'rxjs/operators';



```typescript
import { of } from 'rxjs'; 
import { map } from 'rxjs/operators';

// lets create our data first
const data = of([
  {
    brand: 'porsche',
    model: '911'
  },
  {
    brand: 'porsche',
    model: 'macan'
  },
  {
    brand: 'ferarri',
    model: '458'
  },
  {
    brand: 'lamborghini',
    model: 'urus'
  }
]);

// get data as brand+model string. Result: 
// ["porsche 911", "porsche macan", "ferarri 458", "lamborghini urus"]
data
  .pipe(
    map(cars => cars.map(car => `${car.brand} ${car.model}`))
  ).subscribe(cars => console.log(cars))

// filter data so that we only have porsches. Result:
// [
//   {
//     brand: 'porsche',
//     model: '911'
//   },
//   {
//     brand: 'porsche',
//     model: 'macan'
//   }
// ]
data
  .pipe(
    map(cars => cars.filter(car => car.brand === 'porsche'))
  ).subscribe(cars => console.log(cars))
```



# RxJS MergeMap

https://medium.com/@luukgruijs/understanding-rxjs-map-mergemap-switchmap-and-concatmap-833fc1fb09ff

Now let’s say there is a scenario where we have an Observable that emits an array, and for each item in the array we need to fetch data from the  server.

We could do this by subscribing to the array, then setup a map that calls a function which handles the API call and then subscribe to the result.  This could look like the following:

```typescript
import { of, from } from 'rxjs'; 
import { map, delay } from 'rxjs/operators';

const getData = (param) => {
  return of(`retrieved new data with param ${param}`).pipe(
    delay(1000)
  )
}

from([1,2,3,4]).pipe(
  map(param => getData(param))
).subscribe(val => console.log(val);
```

To further clarify this: we have `from([1,2,3,4])` as our ‘outer’ Observable, and the result of the `getData()` as our ‘inner’ Observable. In theory we have to subscribe to both our  outer and inner Observable to get the data out. This could like this:

```typescript
import { of, from } from 'rxjs'; 
import { map, delay } from 'rxjs/operators';

const getData = (param) => {
  return of(`retrieved new data with param ${param}`).pipe(
    delay(1000)
  )
}

from([1,2,3,4]).pipe(
  map(param => getData(param))
).subscribe(val => val.subscribe(data => console.log(data)));
```

MergeAll takes care of subscribing to the ‘inner’ Observable so that we  no longer have to Subscribe two times as mergeAll merges the value of  the ‘inner’ Observable into the ‘outer’ Observable. This could look like this:

```typescript
import { of, from } from 'rxjs'; 
import { map, delay, mergeAll } from 'rxjs/operators';

const getData = (param) => {
  return of(`retrieved new data with param ${param}`).pipe(
    delay(1000)
  )
}

from([1,2,3,4]).pipe(
  map(param => getData(param)),
  mergeAll()
).subscribe(val => console.log(val));
```

This already is much better, but as you might already guessed mergeMap  would be the best solution for this. Here’s the full example:

```typescript
import { of, from } from 'rxjs'; 
import { map, mergeMap, delay, mergeAll } from 'rxjs/operators';

const getData = (param) => {
  return of(`retrieved new data with param ${param}`).pipe(
    delay(1000)
  )
}

// using a regular map
from([1,2,3,4]).pipe(
  map(param => getData(param))
).subscribe(val => val.subscribe(data => console.log(data)));

// using map and mergeAll
from([1,2,3,4]).pipe(
  map(param => getData(param)),
  mergeAll()
).subscribe(val => console.log(val));

// using mergeMap
from([1,2,3,4]).pipe(
  mergeMap(param => getData(param))
).subscribe(val => console.log(val));

```

# RxJS SwitchMap

https://medium.com/@luukgruijs/understanding-rxjs-map-mergemap-switchmap-and-concatmap-833fc1fb09ff

SwitchMap has similar behaviour in that it will also subscribe to the inner  Observable for you. However switchMap is a combination of switchAll and  map. SwitchAll cancels the previous subscription and subscribes to the  new one. For our scenario where we want to do an API call for each item  in the array of the ‘outer’ Observable, switchMap does not work well as  it will cancel the first 3 subscriptions and only deals with the last  one. This means we will get only one result. The full example can be  seen here:

```typescript
import { of, from } from 'rxjs'; 
import { map, delay, switchAll, switchMap } from 'rxjs/operators';

const getData = (param) => {
  return of(`retrieved new data with param ${param}`).pipe(
    delay(1000)
  )
}

// using a regular map
from([1,2,3,4]).pipe(
  map(param => getData(param))
).subscribe(val => val.subscribe(data => console.log(data)));

// using map and switchAll
from([1,2,3,4]).pipe(
  map(param => getData(param)),
  switchAll()
).subscribe(val => console.log(val));

// using switchMap
from([1,2,3,4]).pipe(
  switchMap(param => getData(param))
).subscribe(val => console.log(val));

```

While switchMap wouldn’t work for our current scenario, it will work for other scenario’s. It would for example come in handy if you compose a  list of filters into a data stream and perform an API call when a filter is changed. If the previous filter changes are still being processed  while a new change is already made, it will cancel the previous  subscription and start a new subscription on the latest change. An  example can be seen here:

```typescript
import { of, from, BehaviorSubject } from 'rxjs'; 
import { map, delay, switchAll, switchMap } from 'rxjs/operators';

const filters = ['brand=porsche', 'model=911', 'horsepower=389', 'color=red']
const activeFilters = new BehaviorSubject('');

const getData = (params) => {
  return of(`retrieved new data with params ${params}`).pipe(
    delay(1000)
  )
}

const applyFilters = () => {
  filters.forEach((filter, index) => {

    let newFilters = activeFilters.value;
    if (index === 0) {
      newFilters = `?${filter}`
    } else {
      newFilters = `${newFilters}&${filter}`
    }

    activeFilters.next(newFilters)
  })
}

// using switchMap
activeFilters.pipe(
  switchMap(param => getData(param))
).subscribe(val => console.log(val));

applyFilters()

```



# Forms

## Dynamic FormArray

https://www.bitovi.com/blog/managing-nested-and-dynamic-forms-in-angular

https://www.tektutorialshub.com/angular/nested-formarray-example-add-form-fields-dynamically/