---
title: Home
---

**Abitbol Serializable** is an [abitbol][] class that can serialize its
properties.

**Features:**

* Serialize / Unserialize all computed properties that have a getter and
  a setter,
* Skip properties annotatated with `"@serializable false"`.
* Use custom serialization function for specific properties.

**Example Class:**

```javascript
var SerializableClass = require("abitbol-serializable");

var Person = SerializableClass.$extend({

    __name__: "Person",  // The class name

    __init__: function(params) {
        this.$data.firstName = "John";
        this.$data.lastName = "DOE";
        this.$data.age = 0;
        this.$super(params);
    },

    getFirstName: function() {
        return this.$data.firstName;
    },

    setFirstName: function(firstName) {
        this.$data.firstName = firstName;
    },

    getLastName: function() {
        return this.$data.lastName;
    },

    setLastName: function(lastName) {
        this.$data.lastName = lastName;
    },

    getAge: function() {
        "@serializable false";
        return this.$data.age;
    },

    setAge: function(age) {
        this.$data.age = age;
    }

});
```

**Example Serialization:**

```javascript
var john = new Person({
    lastName: "Wayne",
    age: 72
});

john.serialize();

// -> {
//        __name__: "Person",
//        id: "<an autogenerated uuid>",
//        firstName: "John",
//        lastName: "Wayne"
//    }
```


[abitbol]: https://wanadev.github.io/abitbol/using-abitbol.html