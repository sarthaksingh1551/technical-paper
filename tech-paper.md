# **What is Design Pattern?**
In software design language, a pattern is a reusable solution which a programmer uses to solve commonly occurring problems. In other words, patterns are templates for solving a problem that can be used in different situations. [*[1]*](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)
#


# **Design Patterns used in JavaScript**

## Module design pattern
JavaScript modules are the most prevalently used design patterns for keeping particular pieces of code independent of other components. This provides loose coupling to support well-structured code.

In JavaScript, modules are “classes”. One of the many advantages of classes is encapsulation - it is used to protect the states and behaviors from being accessed from other classes.

Modules ought to be Immediately-Invoked-Function-Expressions (IIFE) to take into account private scopes - that is, a conclusion that ensures protection of variables and methods (in any case, it will return an object rather than a function). [*[2]*](https://www.digitalocean.com/community/tutorial_series/javascript-design-patterns)

This is what it resembles:

```javascript
(function () {
    // declare private variables and/or functions

    return {
        // declare public variables and/or functions
    }

})();
```
Here we initialize the private variables and/or functions prior to returning our object that we need to return. Code outside of our conclusion can't get to these private variables since it is not in the same scope. How about we bring it into execution:

Here is one javascript file, lets call it languages.js:

```javascript
class programmingLanguages {
    constructor() {
        // private properties
        this.langList = ['Python', 'JavaScript', 'Java']
    }

    // public methods
    getLangList() {
        return this.langList.join(", ")
    }

    addLang(Language) {
        this.langList.push(language)
    }
}
export default programmingLanguages; // This will export the class so that we can use it in different files.
```

Let us look at another javascript file to use the class programmingLanguages. Let us call it main.js:

    import programmingLanguages from "file-location";

    var language = new programmingLanguages;
    console.log(language.getlangList());

This will allow the user to print the programming language list in the other file (here main.js) using the Module Design Pattern.


## Observer Design Pattern
There are ordinarily when one part of the application changes, different parts should be refreshed. In AngularJS, if the $scope object refreshes, an occasion can be set off to advise another part. The observer pattern joins simply that - if an object is adjusted, it broadcasts to subordinate objects that a change has happened.

Another prime example is the model-view-controller (MVC) architecture; The view updates when the model changes. One benefit is decoupling the view from the model to reduce dependencies.

Another perfect representation of observer pattern is the model-view-controller (MVC) architecture; When the model changes, the view refreshes. One advantage is decoupling the view from the model to diminish conditions. [*[2]*](https://www.digitalocean.com/community/tutorial_series/javascript-design-patterns)

>> Observer Design Pattern ![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8d/Observer.svg/1000px-Observer.svg.png)

Let’s see how this is implemented:

```javascript
var Subject = function () {
    this.observers = [];

    return {
        subscribeObserver: function (observer) {
            this.observers.push(observer);
        },


        notifyAllObservers: function () {
            for (var i = 0; i < this.observers.length; i++) {
                this.observers[i].notify(i);
            };
        }
    };
};

var Observer = function (number) {
    return {
        notify: function () {
            console.log("Observer " + number + " is notified!");
        }
    }
}

var subject = new Subject();

var observer1 = new Observer();
var observer2 = new Observer();
var observer3 = new Observer();

subject.subscribeObserver(observer1);
subject.subscribeObserver(observer2);
subject.subscribeObserver(observer3);

subject.notifyAllObservers();
// Observer 1 is notified!
// Observer 2 is notified!
// Observer 3 is notified!
```

## Prototype Design Pattern
The Prototype design pattern depends on the JavaScript prototypical inheritance. The prototype model is utilized chiefly for making objects in performance-intensive conditions. 

The objects made are clones (shallow clones) of the original object that are passed around. One use instance of the prototype pattern is playing out a broad database activity to create an object utilized for different parts of the application. On the off chance that another process needs to utilize this object, rather than playing out this considerable database activity, it is invaluable to clone the recently created object. [*[2]*](https://www.digitalocean.com/community/tutorial_series/javascript-design-patterns)

To clone an object, a constructor must exist to instantiate the first object. Next, by using the keyword prototype variables and methods bind to the object’s structure. Let’s look at a basic example:

To clone an article, the existence of a constructor is a must to launch the first object. Then, by utilizing the keyword prototype, variables and methods tie to the objects’ structure. How about we take a gander at a fundamental example:

```javascript
var myCar = {
    name = "Bolide",
    manufacturer = 'Bugatti',
    drive: function () {
        console.log("Driving Bugatti Bolide!");
    }
}

var yourCar = Object.create(myCar);

console.log(yourCar.name);
console.log(yourCar.manufacturer);
```

## Singleton Design Pattern
A Singleton Design Pattern limits the number of instances of a particular object to just one. The Singleton confines customers from creating numerous objects, after the principal object is made, it will return instances of itself.

```javascript
var mySingleton = (function () {

    var instance;
    function init() {
        // Private methods and variables
        function myPrivate() {
            console.log("No one can see me");
        }
        var myPrivateVar = "Im also private";
        var myPrivateRandomNumb = Math.random();
        return {
            // Public methods and variables
            myPublic: function () {
                console.log("I am Public");
            },
            publicProperty: "Public! Public! Public!",
            getRandomNumb: function () {
                return myPrivateRandomNumb;
            }
        };
    };
    return {
        // If one Singelton exists, get it
        // If it doesn't exist, create one
        getInstance: function () {
            if (!instance) {
                instance = init();
            }
            return instance;
        }
    };
})();

var X = mySingleton.getInstance();
var Y = mySingleton.getInstance();
X.myPublic();
console.log(X.publicProperty);
console.log(X.getRandomNumb() === Y.getRandomNumb());
```

The myPrivate method is private because we do not want the client to access this, however, notice that the getRandomNumb method is public and returns myPrivateRandomNumb. We can create an instance by associating with the getInstance method, like so:

```javascript
var X = mySingleton.getInstance();
var Y = mySingleton.getInstance();
X.myPublic();
console.log(X.publicProperty);
console.log(X.getRandomNumb() === Y.getRandomNumb());
```

In AngularJS, Singletons are pervasive, the most striking being services, factories, and suppliers. Since they keep upstate and gives asset getting to, generating two instances invalidates the purpose of a common service/factory/provider.

Race conditions happen in multi-threaded applications when more than one thread attempts to get to a similar asset. Singletons are vulnerable to race conditions, to such an extent that assuming no instance has initialized first, two threads could generate two objects as opposed to returning and instance. This nullifies the point of a singleton. Subsequently, developers should be aware of synchronization while carrying out singletons in multithreaded applications. [*[2]*](https://www.digitalocean.com/community/tutorial_series/javascript-design-patterns)



## Mediator Design Pattern
Dictionary references Mediator to a *go-between as an unbiased gathering that aids arrangements and compromise*.

![](https://www.dofactory.com/img/diagrams/javascript/javascript-mediator.jpg)

A certifiable relationship could be an average airport traffic control system. A tower (Mediator) handles what planes can take off and land since all interchanges (instructions being tuned in out for or broadcast) are done from the planes to the control tower, instead of from plane-to-plane. A brought together regulator is vital to the achievement of this framework and that is the job a Mediator plays in a programming plan. [*[1]*](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)

![](https://miro.medium.com/max/1046/1*BJu9_D2BWkEnbOWtjrIdeg.png)

A Mediator is an object that organizes collaborations (logic and conduct) between various objects. It settles on choices on when to call which objects, in view of the activities (or inaction) of different objects and input. 

Before we investigate the example to all the more likely comprehend the mediator design pattern, let us complete a few essentials to help better comprehend it first:

The objects participating in the pattern are:

* **Mediator** - In example: *Whatsappgroup*
    * defines an interface for communicating with Friends objects
    * maintains references to Friends objects
    * manages central control over operations

* **Friends** - In example: *Users*
    * objects that are being mediated by the Mediator
    * each instance maintains a reference to the Mediator

Lets now dive into the example of Mediator Design Pattern:

```javascript
var User = function (name) {
    this.name = name;
    this.whatsappgroup = null;
};

User.prototype = {
    send: function (message, to) {
        this.whatsappgroup.send(message, this, to);
    },
    receive: function (message, from) {
        log.add(from.name + " to " + this.name + ": " + message);
    }
};

var Whatsappgroup = function () {
    var users = {};

    return {

        register: function (user) {
            users[user.name] = user;
            user.whatsappgroup = this;
        },

        send: function (message, from, to) {
            if (to) {                      // single message
                to.receive(message, from);
            } else {                       // broadcast message
                for (type in users) {
                    if (users[type] !== from) {
                        users[type].receive(message, from);
                    }
                }
            }
        }
    };
};

// log helper

var log = (function () {
    var log = "";

    return {
        add: function (msg) { log += msg + "\n"; },
        show: function () { alert(log); log = ""; }
    }
})();

function run() {
    var arnav = new User("Arnav");
    var farhan = new User("Farhan");
    var daksh = new User("Daksh");
    var raghav = new User("Raghav");

    var whatsappgroup = new Whatsappgroup();
    whatsappgroup.register(arnav);
    whatsappgroup.register(farhan);
    whatsappgroup.register(daksh);
    whatsappgroup.register(raghav);

    arnav.send("All you need is friends.");
    arnav.send("I love hanging out with you Farhan.");
    farhan.send("Hey, no need to broadcast", arnav);
    daksh.send("Ha, I heard that!");
    raghav.send("Daksh, what do you think?", daksh);

    log.show();
}
```

In the above code, we have 4 users who are joining a chat session by registering with a Whatsappgroup ( the Mediator). Each user is represented by a User object. Users send messages to each other and the Whatsappgroup handles the routing.
#

# Conclusion
Design patterns are now and again utilized in larger applications. However, to comprehend where one may be worthwhile over another accompanies practice. 

Prior to building any application, you ought to completely consider every entertainer and how they associate with each other. In the wake of checking on the Module, Prototype, Observer, and Singleton designs pattern, you ought to have the option to recognize these patterns and use them in nature.
#

# References
1.  Learning JavaScript Design Patterns - Addy Osmani
(Volume 1.7.0)

2. JavaScript Design Patterns - Devan Patel (digitalocean.com)