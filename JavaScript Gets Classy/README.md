# JavaScript Gets Classy

ES6 formally introduced classes to JavaScript, along with a range of other long-awaited features. While classes are not strictly necessary and can be described as *syntactical sugar*, they are incredibly useful in allowing users to create clean and efficient code. In this post, we'll take a look at some of the key features of JavaScript classes, and how we can use them effectively.


## Introduction of Classes in JavaScript

While classes are considered to be one of the key components of object-oriented programming (OOP), they did not officially appear in JavaScript until 2015. Until then, users were able to achieve the same functionality using functions and prototype delegations (you can read more about prototypal inheritance [here](https://coryrylan.com/blog/javascript-prototypal-inheritance)), however it was not until the release of [ES6 (ECMAScript 6)](http://es6-features.org/) that the class keyword finally became available. There were a number of reasons for this change. The new syntax is considered to be cleaner and more intuitive - for instance, we can clearly define classes using the class keyword, we have a constructor method to initialise our objects, and we can create specific class methods. Additionally, because classes exist in other languages such as Java, C++, and Ruby, many developers desired more consistency between coding languages, which ES6 went some way towards achieving.

*Side note: ES6 has also provided JavaScript users with a variety of other features, including arrow functions, destructuring assignment, and template literals. If you'd like to know more, check out a full list of new ES6 features [here](http://es6-features.org/).*

<br>

## Why Do We Use Classes?

Classes can be thought of as a sort of blueprint or template for creating objects. They can be used to manage the initialisation of instances of that class, and we can determine what attributes we want to include when creating objects. Classes provide a way for us to define inheritance, and we can also create methods to be used throughout the class, minimising the need for repetitious code.

<br>

## Features of JavaScript Classes

JavaScript classes share most of conventional aspects that you've probably encountered when using classes in other languages. Here, we'll examine some of the most important features.

<br>

### Class Keyword

Classes in JavaScript are now defined using the **class** keyword and the chosen name of the class, like so:

```javascript
class Country {}
```

<br>

It's not necessary for you to directly give your class a name. Instead, you could assign your class to a variable:

```javascript
const Country = class {}
```
<br>

Now that we've created our class, we're able to explore what we can do with it.

<br>

### Class Constructor

In the above example, we created valid a JavaScript class. However, this is not especially useful *yet*, as it doesn't contain any information. Generally, when we're creating classes, we want to define the attributes that we've deemed essential for instances of that class. We can do that by using the **constructor** method, which allows us to pass in arguments when we create a new instance of that class, and attaches that data as attributes of our instance.

Below, we've created a Country class, and we've decided that the attributes that are most important to us include the name of the country, the continent where that country is located, the colours of that country's flag, the national day, and the national animal. It's important to note that these attributes are created using the **this** keyword. **this** refers to the object it is contained within, so here we are essentially stating that, for instance, the countryName property of *this* object is to be set to the first argument we pass in. You can find more on **this** [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this).

```javascript
class Country {

    constructor(countryName, continent, flagColours, nationalDay, nationalAnimal) {
      this.countryName = countryName
      this.continent = continent
      this.flagColours = flagColours
      this.nationalDay = nationalDay
      this.nationalAnimal = nationalAnimal
    }

}
```
<br>

Et voilà! We've defined our class attributes. However, classes don't really do anything by themselves, and we need to create instances in order to make them useful. An instance is an object which contains data and behaviour defined by the class to which it belongs. In JavaScript, can create an instance like so:

```javascript
let scotland = new Country();
```

<br>

While we now have a new instance of the Country class, it still doesn't really do much, as we haven't attached any information to it. In order to really make use of our class, we should create our instance using attributes.

```javascript
let scotland = new Country ("Scotland", "Europe", "Blue and White", "November 30th", "Unicorn")
```

<br>

Something to bear in mind when creating instances (and actually when doing anything in JavaScript that involves arguments), is **arity**, which refers to the number of arguments you pass into a function. In many coding languages, if a certain number of arguments is expected when, we'll get an error message if we provide too many or too few. For example, we can create a similar class in Ruby:

```ruby
class Country

  def initialize(country_name, continent, flag_colours, national_day, national_animal)
      @country_name = country_name
      @continent = continent
      @flag_colours = flag_colours
      @national_day = national_day
      @national_animal = national_animal
  end

end
```

<br>


If we tried to initialise an instance of this class using the wrong number of arguments, we'd have a problem:

```ruby
scotland = Country.new("Scotland")
// ArgumentError (wrong number of arguments (given 1, expected 5))
```

<br>

However, with JavaScript, we're able to create an instance with as many or as few arguments as we like, for instance: 

```javascript
let scotland = new Country ("Scotland")
// LOG: Country {countryName: "Scotland", continent: undefined, flagColours: undefined, nationalDay: undefined, nationalAnimal: undefined}
```

<br>

We can always go back and update this object at a later time, like so: 

```javascript
scotland.continent = "Europe"
// LOG: Country {countryName: "Scotland", continent: "Europe", flagColours: undefined, nationalDay: undefined, nationalAnimal: undefined}
```

<br>

### Class Methods

While we generally talk about functions in JavaScript, they are referred to as methods when they belong to classes. When we create methods within our classes, these can be called upon any instance of that class. For instance, if we wanted to give people a way to get all of the information we have on a certain country, we could create a countryInfo() method:

``` javascript
class Country {

    constructor(countryName, continent, flagColours, nationalDay, nationalAnimal) {
      this.countryName = countryName
      this.continent = continent
      this.flagColours = flagColours
      this.nationalDay = nationalDay
      this.nationalAnimal = nationalAnimal
    }
   
    countryInfo() {
      console.log(`Country: ${this.countryName}`)
      console.log(`Continent: ${this.continent}`)
      console.log(`Flag Colours: ${this.flagColours}`)
      console.log(`National Day: ${this.nationalDay}`)
      console.log(`National Animal: ${this.nationalAnimal}`)
    }

}
```

<br>

As soon as we have instances of that class available, we can call them like so:

```javascript
let scotland = new Country ("Scotland", "Europe", "Blue and White", "November 30th", "Unicorn")

scotland.countryInfo()
// LOG: Country: Scotland
// LOG: Continent: Europe
// LOG: Flag Colours: Blue and White
// LOG: National Day: November 30th
// LOG: National Animal: Unicorn
```

<br>

Creating methods which are available to all members of a class can be extremely powerful, and this is an important feature in making JavaScript classes so convenient.

### Class Inheritance

One of the most useful aspects of a class is the ability to allow it to inherit properties from another class. For instance, we could create a new City class. We know that cities belong to countries, so it would make sense if our City class inherited from our Country class. We can define this relationship by using the **extends** keyword. We create our class as normal and then add **extends** and the name of the class we want this new class to inherit from. We also need to use the **super** keyword. **super** allows the child class to call the constructor of the parent class, and to access its properties and methods. In this example, City is inheriting from Country:

``` javascript
class City extends Country {

    constructor(countryName, continent, flagColours, nationalDay, nationalAnimal, cityName, cityMotto) {
      super(countryName, continent, flagColours, nationalDay, nationalAnimal)
      this.cityName = cityName
      this.cityMotto = cityMotto
    }

}

```

<br>

We can create instances and methods as with any other class, however the new child class not only has access to any methods we create within it, but can also utilise methods within its parent class. In the example below, we can see that the cityInfo() method is using the countryInfo() method defined in the parent Country class.

<br>

``` javascript
class City extends Country {

    constructor(countryName, continent, flagColours, nationalDay, nationalAnimal, cityName, cityMotto) {
      super(countryName, continent, flagColours, nationalDay, nationalAnimal)
      this.cityName = cityName
      this.cityMotto = cityMotto
    }

    cityInfo() {
      console.log(`City Name: ${this.cityName}.`)
      console.log(`City Motto: ${this.cityMotto}.`)
      this.countryInfo()
    }

}

let glasgow = new City (scotland.countryName, scotland.continent, scotland.flagColours, scotland.nationalDay, scotland.nationalAnimal, "Glasgow", "Let Glasgow Flourish")
glasgow.cityInfo()
// LOG: City Name: Glasgow
// LOG: City Motto: Europe
// LOG: Country: Scotland
// LOG: Continent: Europe
// LOG: Flag Colours: Blue and White
// LOG: National Day: November 30th
// LOG: National Animal: Unicorn
```

<br>

### Static Methods

Within classes, we also have the ability to define **static** methods. These are defined using the **static** keyword, and are methods which are called directly on a class. We've defined two static methods in the example below. Rather than, for instance, calling scotland.numberOfCountries(), you would call this directly on the class within which it is defined, Country.

``` javascript
class Country {

    constructor(countryName, continent, flagColours, nationalDay, nationalAnimal) {
      this.countryName = countryName
      this.continent = continent
      this.flagColours = flagColours
      this.nationalDay = nationalDay
      this.nationalAnimal = nationalAnimal
    }

    static numberOfCountries() {
      console.log("There are 195 countries in the world today.")
    }
   
    static continent(country) {
      console.log(`${country.countryName} is located in ${country.continent}.`)
    }
    
}

let scotland = new Country ("Scotland", "Europe", "Blue and White", "November 30th", "Unicorn")
Country.numberOfCountries()
// LOG: There are 195 countries in the world today.
Country.continent(scotland)
// LOG: Scotland is located in Europe.
```

<br>

### Getters, Setters, and Private Properties

Finally, we can take a look at getters and setters in JavaScript classes. Generally, getters are used when we want to access a property that returns a value that requires dynamic computation. Setters are used when we need to ensure that a function is executed whenever a user tries to change a specific property.

As is shown here, we can define getters and setters by using the **get** and **set** keywords:

```javascript
class Country {

    constructor(countryName, continent, flagColours, nationalDay, nationalAnimal) {
      this._countryName = this.titleCase(countryName);
      this.continent = continent
      this.flagColours = flagColours
      this.nationalDay = nationalDay
      this.nationalAnimal = nationalAnimal
    }

    get countryName() {
      return this._countryName.titleCase(this._countryName);
    }
 
    set countryName(countryName) {
      this._countryName = this.titleCase(this.countryName);
    }

    titleCase(countryName) {
      return countryName.charAt(0).toUpperCase() + countryName.slice(1);
    }
    
}
```

<br>

The addition of a getter and a setter isn't the only difference here. We can also see that an underscore has been added before countryName. In many coding languages, we're able to classify certain properties as being private (i.e. properties that are inaccessible from outside the class), simply by using the **private** keyword. Technically, we can't do this in JavaScript, however users have developed the convention of using an underscore to denote a private variable. This doesn't actually prevent a property from being altered - you can still mutate it by using, in this example, _countryName, however, using the underscore shows your intention to other developers, and tells them that you don't want that variable to be accessible.

<br>

## Conclusion

Classes are one of the newest features of JavaScript and have been a valuable addition to the language. While we've covered some of the basics in this post, this just scrapes the surface of what is now available to us as users of JavaScript. You can also find some other useful links below to help guide you through your adventures with JavaScript. Happy coding!

<br>

## Sources  

https://www.developintelligence.com/blog/2016/06/why-do-es6-classes-exist-and-why-now/
https://everyday.codes/javascript/please-stop-using-classes-in-javascript/
http://es6-features.org/
https://www.w3schools.com/jsref/jsref_class_super.asp
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static
https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes
https://coryrylan.com/blog/javascript-prototypal-inheritance