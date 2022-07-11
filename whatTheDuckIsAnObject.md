# whatTheDuckIsAnObject
This is an object: {}. Ok? Easy, now we can move on. <br/>
 
jk read this:
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
 
 
## best practice
Although you are able to make an object on the fly, I firmly believe that it is best to do it in this format regardless of how insignificant the object is. This allows for clarity in reading the code although they compile to the same thing.
 
```js
class ClassName {
   //1
   isClassName = true;
  
   //2
   constructor(props={}) {
       //3
       this._secret = props.secret     || defaultValue;
       this._secret2 = props.secret2   || undefined;
 
       //public
       this.field1 = props.field1      || defaultValue;
       this.field2 = undefined         || defaultValue;
 
       //code...
       this.field2 = resultOfCode; //assign
   }
 
   method() {
       //7
       help(this);
   }
}
 
//4
ClassName.staticMethod = function() {}
 
//5
ClassName.validateField1 = function() {
   return true;
}
 
//6
function help(arguments) {}
```
 
#### comments
1. This is extremely useful for defining what type of object we are dealing with. I like putting it here instead of the constructor because it makes it easier to verify that it is placed in every object.
 
2. You should always pass props in rather than arguments. Js has got a fancy thing called JSON. So for the most part data input and output should be expected in that format. Meaning, using props makes the use of JSON easy.
 
3. private fields should be sudo private so that they are accessible using Object functionality. Notice props.secret is not a secret until it's assigned.
 
4. static methods should be attached externally following the declaration of the class. In fact I think that the static version of the class should be thought of as a separate class entirely... a class that provides functions more so then methods. use function instead of an arrow function to make sure that "this” is defined correctly
 
5. input validation should not be done with setters and getters. It occurs often enough that you have edge cases in which you might want to do something slightly out of the ordinary. Like leaving a field undefined.
 
6. helpers should be declared as functions at the bottom of the page. This keeps the scope of "this” if a method is passed from one object to another from struggling as it wont demand this functionality exist on every object arguments can be handled
 
7. passing in "this" as an argument allows functions to not be dependent on the "this" keyword, just the props attached. there are other ways of handling "this" as well.
 
#### closing thoughts
notice here how this format allows for a few things. The first is clarity in what the object is. the second is that at a glance we are able to quickly tell what the object contains. Object type at the top, private fields, fields, then core functionality. Nothing is hidden behind confusing setters, getters or private methods. It allows for easy debugging and encourages more functional programming which has less “hard to fix bugs” imo.
 
#### argument points
There are two big argument points that I lose sleep over. The first of which is the best way to handle private helpers. There are many ways to do it but they often either obfuscate the code or remove functionality. I felt this one allowed for the most benefits. although it's a bit annoying to have the function
 
The second one is handling input validation. I feel that requirements for classes change so often that adding constraints tends to hurt you more later down the road. As a result, having validation statistics allows the user to call those functions anytime they are getting input from the user and when they are returning it to the backend. I don't think it really matters how classes are used within the js code. It's just the entry and exit points that validation is needed.
 
### pro gamer tips
- you might want to add an Object.prototype for removing the sudo private identifier for when you are printing the obj or saving it to a database.
 
- think of different ways you can pass "this" around in helper functions or maintain the current scope.
 
### do your own research
 
- learn about how the programmers of old used "that" as a reference to "this"
 
- look up all the elements in the prototype chain and research them.
 
- learn the different ways to initialize and object.
 
- learn about method factories
 
- learn about prototypes