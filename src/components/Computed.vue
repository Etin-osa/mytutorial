<template>
  <div class="computed-prop">
    <input type="text" v-model="fullname"/>
    <h1>{{ firstname }}</h1>
    <h1>{{ lastname }}</h1>
  </div>
</template>

<script>

/*

    In this Vue file we’ll see what are computed properties, how to write a computed property and let’s understand how a computed property is designed behind the scenes.

What are the computed properties?
    Computed properties can be used to do quick calculations of properties that are displayed in the view. These calculations will be cached and will only update when needed, Computed properties are like normal methods in Vue, but with the caching ability on the reactive dependencies.


Basic Examples
HTML
<div class="computed-prop">
  FirstName: <input type="text" v-model="firstname">
  lastName: <input ty.
  pe="text" v-model="lastname">
  <h1>My name is {{ firstname }} {{ lastname }}</h1>
  <h1>Using computed method: {{ getFullName }} </h1>
</div>

SCRIPT
data () {
  return {
    firstname: '',
    lastname: '',
  }
},

computed: {
  getFullName() {
    return this.firstname + " " + this.lastname
  }
}

    When we type in the textbox the same is returned by the function, when the properties firstname or lastname is changed. Thus, with the help of computed we don’t have to do anything specific, such as remembering to call a function. With computed it gets called by itself, as the properties used inside changes, i.e. firstname and lastname.

Few things to note
    * A more appropiate name for a computed value is a computed property
    * You can think of computed value as a derived value that will be automatically updated whenever one of the underlying values used to calculate it is updated
    * You don't call a computed value(even though it's a function) and it dosen't accept parameters
    * You reference a computed property just like you would a data property



Difference between Computed and Methods

    * Methods don't know if the values used in the function change so they need to run everytime to check.
      i)  they can be triggered by a click event to call a function in the method or etc..

    * Computed properties know if the values (values they depend on) used in the function change so they don't need to run everytime to check, only once!


Basic Example to prove...

    <div class="computed-prop">
      <h1 style="background-color: gray;">Random No from computed property: {{ getrandomno }}</h1>
      <h1>Random No from method: {{ getrandomno1() }}</h1>
      <h1>Random No from method: {{ getrandomno1() }}</h1>
      <h1 style="background-color: gray;">Random No from computed property: {{ getrandomno }}</h1>
      <h1 style="background-color: gray;">Random No from computed property: {{ getrandomno }}</h1>
      <h1 style="background-color: gray;">Random No from computed property: {{ getrandomno }}</h1>
      <h1>Random No from method: {{ getrandomno1() }}</h1>
      <h1>Random No from method: {{ getrandomno1() }}</h1>
    </div>

    methods: {
      getrandomno1() {
        return Math.random()
      }
    },

    computed: {
      getrandomno() {
        return Math.random()
      }
    }


    If we look at the values above, we will see that the random numbers returned from the computed property remains the same irrespective of the number of times it is called. This means everytime it is called, the last value is updated for all. Whereas for a method, it’s a function, hence, everytime it is called it returns a different value.




Computed getter
    <div class="computed-prop">
      <input type="text" v-model="fullname" />
      <h1>{{ firstname }}</h1>
      <h1>{{ lastname }}</h1>
    </div>

    return {
      firstname: 'Terry',
      lastname: 'Ben',
    }

    computed: {
      fullname: {
        get: function() {
          return this.firstname + ' ' + this.lastname 
        }
      }
    }

    In this aspect the computed value (fullname) displayed in the input gets the value of the firstname and lastname and even when changing the value in input nothing changes in the firstname and lastname properties displayed in the h1


Computed setter
    computed: {
      fullname: {
        get: function() {
          return this.firstname + ' ' + this.lastname 
        },

        set: function(name) {
          var fname = name.split(' ')
          this.firstname = fname[0]
          this.lastname = fname[1]
        }
      }
    }

    same example as ''Computed getter'' ||||--> just adding the set method to the computed value

    Now we can update those values(firstname, lastname) using the fullname Computed value displayed in the input in the DOM

*/

  export default {
    name: 'computed-prop',
    data () {
      return {
        firstname: 'John',
        lastname: 'Terry',
      }
    },

    methods: {
      getrandomno1() {
        return Math.floor(Math.random() * 15)
      }
    },

    computed: {
      fullname: {
        get: function() {
          return this.firstname + ' ' + this.lastname;
        },

        set: function(name) {
          var complete = name.split(' ');
          this.firstname = complete[0];
          this.lastname = complete[1];
        }
      }
    }
  }   
</script>

<style>

</style>