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