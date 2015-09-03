# Javascript's 4 Instantiation Methods

There are so many ways to do anything in Javascript and while it's easy to find something that works and stick with it, I'd argue it's worthwhile to understand a little better how this magic works.

Today we'll be looking at ways to instantiate a class structure and if you keep reading, you'll soon be able to differentiate between them. That way, you can speak to the different methods of creating class structures and understand why one may be better than the others.

To keep some semblance of consistency, and to keep myself (and maybe you) entertained across these four approaches, we'll be building up a Batman class. It may not be the class this post deserves, but it's the class this post needs.

<p><img src="./lego-batman.jpg" alt=""></p>

### First up is the Functional Instantiation Pattern

```javascript
var makeBatman = function() {  
  var batman = {};
  batman.age = 38;
  batman.strength = 200;
  batman.fightJoker = function () {
    this.age--;
  };
  batman.workOut = function () {
    this.strength++;
  };
  return batman;
};

var newBatman = makeBatman();
```
The functional instantiation pattern requires that all methods are defined within one master maker function. This means that each instance of Batman will have all of these methods directly on the object. 
While this seems like it makes sense at first, it violates the DRY(Don't Repeat Yourself) commandment that all good coders follow.


Think about it this way, wouldn't it be more efficient if you were raising an army of batmen and instead of having to train each one individually, he (or she) could instinctively know how to work out or fight Joker by sharing some Bat-hivemind? Totally. The next couple of methods are sort of like that.

### Functional Instantiation w/ Shared Methods

```javascript
var makeBatman = function() {  
  var batman = {};
  batman.age = 38;
  batman.strength = 200;
  _.extend(batman, sharedMethods);
  return batman;
};
var sharedMethods = {};
sharedMethods.fightJoker = function () {  
  this.age--;
};
sharedMethods.workOut = function () {  
  this.strength++;
};

var newBatman = makeBatman();
```

This example uses extend from the underscore js library. This approach creates a sharedMethods object, which includes training and fighting the Joker and _extends_ a reference to these sharedMethods onto the Batman class.

Each Batman can have their own age and strength but they will share their training and fighting methods, making your code leaner and faster. Imagine how much more efficient it will be to raise your vigilante batman army!

### Prototypal Instantiation

```javascript
var makeBatman = function() {  
  var batman = Object.create(batmanMethods);
  batman.age = 38;
  batman.strength = 200;
  return batman;
};
var batmanMethods = {};

batmanMethods.fightJoker = function () {  
  this.age--;
};
batmanMethods.workOut = function () {  
  this.strength++;
};

var newBatman = makeBatman();
```

There are some obvious similarities between these last two methods. The difference is where the methods are. In the prototypal pattern, Object.create creates a delegation relationship between the object being created and the object being passed in. 

This means that if an instantiated Batman is called upon to fightJoker, we'll first look for a fightJoker method on the individual Batman but when we don't find one there, we'll be go to the batmanMethods object where the fightJoker method lives. The fightJoker method will be delegated to the batmanMethods object.


Even though this Batman may not have these actions hard-coded in, he has access to them through the batmanMethods he was created with. Think of this as some heriditary instinct that he has. While he may not explicitly have a method for fighting the Joker, when he looks for it, he will find it in the batmanMethods object that he was created with.

This saves space but can also make code a bit more flexible since if a Batman were to have a special fightJoker or workOut method it would take precedence over one that is on the batmanMethods object. Hooray for flexibility!


### Pseudo-Classical Instantiation

```javascript
var Batman = function () {  
  this.age = 38;
  this.strength = 200;
};

Batman.prototype.fightJoker = function () {  
  this.age--;
};
Batman.prototype.workOut = function () {  
  this.strength++;
};

var newBatman = new Batman();
```

### Behold! PseudoClassical Instantiation! 

It is the method that most browsers are optimized for so get comfortable with it.
Most imporant to understand with this method is what's going on up at the top. There's few things happening implicitly in this pattern.
1. `this = object.create(batman)` happens implicitly right at the beginning (_You didn't event have to code it!_)
2. The Batman function return `this`, which is the new batman (_You didn't have to code that either!_)
3. The other thing to pay attention to is that these methods are being added onto the Batman Object prototype. These methods will then be available on every new Batman instance to delegate to if a lookup on the original object fails

Also, you may have noticed that the Batman function starts with a capital B, where the other methods started with a lower-case letter. This is actual best-practices and will let other people reading your code know that you're using Pseudo-Classical instantiation. Additionally, we used the new keyword, which is what tells the parser to implicitly do those magic steps above!

So we've covered all of the above instantiation types and I'd be surprised if you don't run into them in the future. I typically use Pseudo-Classical and as mentioned earlier, it's what most browsers are optimized for.

Now you're off to the races, any questions? lemme know!
<p><img src="./batman-run.gif" alt=""></p>