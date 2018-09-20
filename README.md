# A Quick Exposure to RxJava

In ReactiveX, the core type you will work with is the *Observable*. An Observable pushes things. A given *Observable<T>* pushes things of type *T* through a series of operators until it arrives at an *Observer* that consumes the items. For eg. in code below
  
 ```
 public class Launcher {
 
   public static void main(String[] args) {
   Observable<String> myStrings =
   Observable.just("Alpha", "Beta", "Gamma", "Delta",
   "Epsilon");
   }
}
 ```
In our *main()* method, we have an *Observable<String>* that will push five string objects. An Observable can push data or events from virtually any source, whether it is a database query or live Twitter feeds. In this case, we are quickly creating an Observable
using *Observable.just()*, which will emit a fixed set of items.
 
However, running this *main()* method is not going to do anything other than declare *Observable<String>*. To make this Observable actually push these five strings (which are called emissions), we need an *Observer* to subscribe to it and receive the items.
We can quickly create and connect an *Observer* by passing a lambda expression that specifies what to do with each string it receives:
  
```
public class Launcher {

      public static void main(String[] args) {
      Observable<String> myStrings =
      Observable.just("Alpha", "Beta", "Gamma", "Delta",
      "Epsilon");
      myStrings.subscribe(s -> System.out.println(s));
      }
}
```
The output on running the code is

```
Alpha
Beta
Gamma
Delta
Epsilon
```
What happened here is that our *Observable<String>* pushed each string object one at a time to our Observer, which we shorthanded using the lambda expression `s -> System.out.println(s)`. We pass each string through the parameter s (which I arbitrarily named) and instructed it to print each one. 
Lambdas are essentially mini functions that allow us to quickly pass instructions on what action to take with each incoming item. Everything to the left of the arrow -> are arguments (which in this case is a string we named s), and everything to the right is the action (which is System.out.println(s)).
  
We can also use several operators between *Observable* and *Observer* to transform each pushed item or manipulate them in some way. Each operator returns a new *Observable* derived-off the previous one but reflects that transformation. For example, we can use *map()* to turn each string emission into its *length()*, and each length integer will then be pushed to Observer , as shown in the following code snippet:

```
public class Launcher {

      public static void main(String[] args) {
      Observable<String> myStrings =
      Observable.just("Alpha", "Beta", "Gamma", "Delta",
      "Epsilon");
      myStrings.map(s -> s.length()).subscribe(s ->
      System.out.println(s));
      }
}
```
Output

```
5
4
5
5
7
```
To emphasize again, emissions are pushed one at a time all the way to *Observer*. Emissions represent both data and an event, which can be emitted over time. Of course, beyond map(), there are hundreds of operators in RxJava, Learning which operators to use for a situation and how to combine them is the key to mastering RxJava.

