# whatTheDuckIsAnObject
This is an object: {}. Ok? Easy, now we can move on. <br/>
 
jk read this:
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object
 
 
## best practice
Although you are able to make an object on the fly, I firmly believe that it is best to do it in this format regardless of how insignificant the object is. This allows for clarity in reading the code although they compile to the same thing.
 
```js
//constants
const TIME = 564456126;
const DEFAULT = class {
  public = 'public';
  special = 'special';
}

class Name{
  isName = true;
  
  //the users sees these the same way
  public;
  #special;
  
  //this is not visible to the user
  #private = 'private';
  
  constructor(props) {
    // creats new DEFAULT Object every time we create a new instance of this class.
    props = Object.assign(new DEFAULT(), props);
    
    this.public = props.public;
    this.special = props.special;
  }
  
  get props() {
    return {
      ...super.props, // if this extends an object.
      public: this.public,
      special: this.special,
    }
  }
  
  get special() {
    return this.#special;
  }
  
  set special(v) {
    if(v===undefined) {throw new Error('v undefined');}  // use this validation in setter only if required.
    this.#private = 'updated special';
    this.#special = v;
  }
  
  method(args) {
    return this.#helper(args);
  }

  #helper(args) {
    
  }
}

Name.staticField = [];

Name.staticMethod = (val)=>{
  Name.staticField.push(val);
}
```
