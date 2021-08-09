<template>
  <div class="watcher">
    <h1>{{ counter }}</h1>
    <!--<button @click="updateCounter">Click Me</button>
    <input type="text" v-model="someText">-->
    <button @click="counter++">Click Me</button>
  </div>
</template>

<script>

/*

Vue js Watchers
    * A Vue watcher allow you to listen to the component data and run whenever a particular property changes, 
    * A watcher is a special Vue.js feature that allows you to spy on one property of the component state, and run a function when that property value changes
    * There is one major thing you MUST take note of. The name property within the watch object MUST BE CALLED the name of the property to watch and nothing else

i| Basic example of watch component 

    data () {
      return {
        counter: 0,
      }
    },


    the HTML changing the counter value
        <h1> {{ counter }} </h1>
        <button @click="counter++">Click Me</button>


    The watch property
        watch: {
          counter(newVal, oldVal) {
            console.log(`old value ${oldVal} new value ${newVal} `)
          }
        }

    * The component on the watch to check for the change must have same name as the property it's watching 
    * And it has access to 2 parameters the newValue and the oldValue


ii| Another Example
    data () {
      return {
        someText: 'Hi'
      }
    },

    methods: {
      changeText() {
        this.$data.someText = 'Hello'
      },
      updated() {
        console.log('hurry')
      }
    },

    watch: {
      someText: 'updated'// Watch example 2
    }


Ther are three properties in a watcher
    * Handler
    * Deep
    * immediate
    
    both deep & immediate are boolean and examples will be given

Using handler for example --> i|
    watch: {
      counter: {
        handler(newVal, oldVal) {
        console.log(`old value ${oldVal} new value ${newVal} `)
      }
    }

    for example --> ii|
    watch: {
      someText: {
        handler: 'updated' // Watch example 2
      }
    }




Using deep
    Basically, you use deep when watching for changes in the value of items inside an array, or changes in the value of properties inside an object. You will need to set deep to true in order to tell Vue.js to inspect the contents of arrays and objects.

    HTML
      <h1> {{ someText }} </h1>
      <button @click="fruitsName">Click Me</button>

    data () {
      return {
        someText: 'Hi',
        fruits: [
          { name: 'orange', color: 'orange', price: 1.50 },
          { name: 'mango', color: 'yellow', price: 2.50 },
        ]
      }
    },

    methods: {
      fruitsName() {
        this.fruits[1].name = 'pineapple'
      },
    },

    watch: {
      fruits: {
        deep: true,
        handler() {
          this.someText = this.fruits[1].name
        }
      },
    }





Using immediate
    The immediate property calls the handler before the page is initialized, Even when the change hasn't being made yet   
    
    * Now imagine you want to call a method in the created lifecycle hook
    * And that method changes a property in data
    * And you wish to watch for the change in that data
    * So, basically the lifcycle hook and the watcher calls the same method
    * what the immediate property does is that it does the job of created lifecycle hook without having the need to set it( created lifecycle hook )
  

Without immediate 

    <div class="compatch">
      <h1> {{ counter }} </h1>
      <button @click="updateCounter">Click Me</button> 
      <input type="text" v-model="someText">
    </div>

    return {
      counter: 0,
      someText: '',
    }

    methods: {
      updateCounter() {
        this.counter++
      },
    },

    watch: {
      counter(newVal, oldVal) {
        console.log(`old value ${oldVal} new value ${newVal} `)
      },

      someText: {
        handler: 'updateCounter' // Watch example 2
      }
    },

    created() {
      this.updateCounter()
    }


With immediate
    someText: {
      handler: 'updateCounter',
      immediate: true,
    }

    Created is not needed


*/
export default {
  name: 'watcher',
  data () {
    return {
      counter: 0,
      someText: 'Hi',
    }
  },

  methods: {
    updateCounter() {
      this.counter++
    },

    changeText() {
      this.someText = 'Hello'
    },

    updated() {
      console.log('hurry')
    },

    fruitsName() {
      this.fruits[1].name = 'lemon'
    },
  },

  watch: {
    counter(newVal, oldVal) {
      console.log('old value ' + oldVal + ' new value ' + newVal + '.')
    },

    someText: {
      handler: 'updateCounter',
      immediate: true,
    },
  }
}
</script>

<style>

</style>