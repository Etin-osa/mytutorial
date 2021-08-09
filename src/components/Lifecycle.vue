<template>
  
</template>

<script>
/*

There are 8 lifecycle hooks

    1.  Before create
    2.  Created
    3.  Before mount
    4.  Mounted
    5.  Before update
    6.  Updated
    7.  Before destroy
    8.  Destroyed

    Lifecycle hooks are an important part of any serious component. You often need to know when your component is created, added to the DOM, updated or destroyed

The script section in App.vue will be used for the various hooks illustrations throughout the course of this tutorial.

*/




/*

Creation(Initialization)
    Creation hooks are the very first hooks that run in your component. They allow you to perform actions before your component has even been added to the DOM. Unlike any of the other hooks, creation hooks are also run during server-side rendering.

    Use creation hooks if you need to set things up in your component both during client rendering and server rendering. You will not have access to the DOM or the target mounting element (this.$el) inside of creation hooks.


beforeCreate()
    This is the very first lifecycle hook that gets called in Vue JS, it gets called immediately after the Vue instance has been initialized. Notice that the alert statement written inside the lifecycle hook executed first before the component loaded. This is exactly the function: to be called before Vue engine creates the app component. This way at the beforeCreate stage, things like computed properties, watchers, events, data properties , and manipulation are not set up yet.

    beforeCreate() {
      alert('beforCreate hook has being called')
      console.log('beforCreate hook has been called')
    }


Created()
    This is, as you have guessed, the second lifecycle hook that is called right after the beforeCreated hook. At this stage, the Vue instance has been initialized and has activated the start of things like computed properties, watchers, events, data properties and manipulations that come with it, Vitual DOM not yet been mounted or rendered

    data() {
      return {
        books: 0
      }
    },
    created() {
      alert('Created hook has being called')
      console.log(`books is of type ${typeof this.books}`)
    }

    If you run the application you will quickly notice that the type of data can now be displayed. It was not possible at the beforeCreated stage because the activation that takes place here has not taken place at the time. However, the Vue instance has not been mounted at this stage so you cannot manipulate the DOM here, the element(this.$el) property is not available for use yet.

*/




/*

Mounting (DOM Insertion)
    Mounting hooks are often the most-used hooks, for better or worse. They allow you to access your component immediately before and after the first render. They do not, however, run during server-side rendering.

    Use if: You need to access or modify the DOM of your component immediately before or after the initial render.

    Do not use if: You need to fetch some data for your component on initialization. Use created (or created + activated for keep-alive components) for this instead, especially if you need that data during server-side rendering.



beforeMount()
    This is the next lifecycle hook that gets called after the created hook is called. This is the moment immediately before the instance is mounted on the DOM, the template and the scoped styles are all compiled here but you still cannot manipulate the DOM yet, the element property is not still available. Here is where initializations that you do not want lying around in your component should go into:

    beforeMount() {
      alert('beforeMount is called')
    }




Mounted()
    This is the next lifecycle hook to be called after the beforeMounted is called. It is called right after the instance has been mounted. Here the app component, or any other component in the project becomes functional and can now be used. The data is fit into the template, the DOM element is replaced with data filled element and can now be manipulated here, the element property is now available for use.

    Mounted is the most-often used lifecycle hook. You will have full access to the reactive component, templates, and rendered DOM (via. this.$el --> the element property) 

    mounted() {
      alert('mounted has been called'); 
    }

    This is the default place any project created with the Vue CLI is at because the mounting is already done in the main.js file as we saw in the beginning. This is why you may not get to use the other hooks because the instance is already mounted by default for you.

*/




/*

Updating (Diff & Re-render)
    Updating hooks are called whenever a reactive property used by your component changes, or something else causes it to re-render. They allow you to hook into the watch-compute-render cycle for your component.

    Use if: You need to know when your component re-renders, perhaps for debugging or profiling.

    Do not use if: You need to know when a reactive property on your component changes. Use computed properties or watchers for that instead.



beforeUpdate()
    This is the lifecycle hook called after the mounted hook, anytime a change is made to the data that requires the DOM to be updated. This stage is great for any logic before data changes like removing an event listener.

      <template>
        <div> {{hello}} </div>
      </template>

      data() {
        return {
          hello: 'welcome to Vue JS'
        }
      },
      beforeUpdate(){
        alert('beforeUpdate hook has been called');
      },
      mounted(){
        this.$data.hello= 'lalalalallalalalalaalal';
      }

    This originally has a welcome note on the DOM but in the mounted stage (which is where the DOM can be manipulated), the data gets changed and so the alert for beforeUpdate appears just before it changes.




updated()
    This lifecycle hook is called just after a DOM update has occurred, so this means immediately after the beforeUpdate hook is called. DOM related operations can be performed here, although it is not advisable to change state inside this hook as Vue already provides platforms specifically for that.

    add this to the lifecycle example at beforeUpdate
    updated(){
      alert('Updated hook has been called');
    },

*/




/*

beforeDestroy()
    This Vue lifecycle hook is called just before a Vue instance is destroyed, the instance and all the functionalities are still intact and working here. This is the stage where you can do resource management, delete variables and clean up the component or reactive subscriptions.

    beforeDestroy() {
      this.books = null
      delete this.books
    }

*/




/*

Destruction (Teardown)
    Destruction hooks allow you to perform actions when your component is destroyed, such as cleanup or analytics sending. They fire when your component is being torn down and removed from the DOM.



destroyed()
    This is the final stage of the Vue lifecycle where all the child Vue instances have been destroyed, things like event listeners and all directives have been unbound at this stage. It gets invoked after running destroy on the object.

    destroyed() {
      this.$destroy() 
      console.log(this)
    }
    
    When you run the app and take a look at the console, you will see nothing.

*/









/*

Other Hooks
There are two other hooks, activated and deactivated. These are for keep-alive components, a topic that is outside the scope of this article. Suffice it to say that they allow you to detect when a component that is wrapped in a <keep-alive></keep-alive> tag is toggled on or off. You might use them to fetch data for your component or handle state changes, effectively behaving as created and beforeDestroy without the need to do a full component rebuild.

*/
export default {

}
</script>

<style>

</style>