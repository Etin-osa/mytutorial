<template>
  <ul>
    <li v-for="fruit in fruits" :key="fruit.id">
      <slot name="fruit" :fruit="fruit" :slice="slice" /> 
      <slot name="recipe" :fruit="fruit" />
    </li>
  </ul>
</template>

<script>

/*

    What is slot
    Slots are reserved space offered by vuejs to display content passed down from one component to another. There are two types of slot in vuejs namely: named slot and unnamed(default) slot.

    Practical Use Case
    • To pass down Html elements from one component to another.

    With props, vue allows us to pass strings, objects, arrays and functions from a parent component to its child component. While it is possible for us to pass html elements from a parent to it child component as string this will make our website vulnerable to cross site scripting attack that is why vuejs provides us with slot which is a more secure and reliable method of passing html element and other contents from parent to its child component for rendering.

    How to Use Slot
    In the child component where the content is to be displayed, add the slot tag as follows:

    Add the code below to child.vue in our case(Slts.vue)

<div>
    <div>
      <h2>Child Component</h2>
    </div>
</div>

    Add the code snippet below to parent.vue in our case(App.vue)

<div>
  <h2>Parent</h2>
  <Slts>
    <h3 class="child-content">You are my first child</h3>
    <h4 class="child-content">Your name is Tom</h4>
  </Slts>
</div>



    Here we imported the child component and pass down the html content to the child.
    For these contents to be displayed in the child component, the slot tag must be added to the child component.
<div>
  <h2>Child Component</h2>
  <slot></slot>
</div>

    The context written in the parent component in place of slots(in the child component) can access data in the parent element, example from one the element passed in slot
<h4 class="child-content">Your name is Tom {{ Mark }} </h4> // Mark being a data property in the parent.Vue

*/




/*

    The Default Slot

    When you do not specify any name in your slot, Vue will do it for you and call it “default.”
    In the example below, we also defined some fallback content. This will appear when we didn’t define any content in the parent component. You can leave the <slot /> tag empty if you don’t need the fallback to be displayed.

    Parent component
<Slts>
  <h1>I am injecting some content in the default slot</h1>
</Slts>


    Child component
<div class="my-child-component">
  <slot>
    <h1>
      When no slot is specified in the parent, this fallback text will appear.
    </h1>
  </slot>
</div>

*/



/*

    Styling Slot Component

    For styling our slot component, the css styles should be added to the component with the slot tag.
    So in child.vue component we will add the following styles to the html content received from the parent.vue component.

.child-content {
  background-color: blue;
  color: red;
}

*/





/*

    Using Multiple Slots

    In order to use multiple slots in vue, vuejs provides us with a way to name our slots.
    What if we want the h2 and h3 tags in the parent component to be displayed individually in separate slots. This would be a typical use case for named slots.

    From the first example in the Parent component
<h3 class="child-content" slot="message">You are my first child</h3>
<h4 class="child-content" slot="name">Your name is Tom</h4>


    In the child.vue component
<slot name="message"></slot>
<slot name="name"></slot>

    You can also add in the name in the parent component using v-slot or '#slotName' as long as it's in template 
<h4 class="child-content" v-slot="name">Your name is Tom</h4>
    or 
<template #message>hi long time</template> || <template #childy><p>hi long time</p></template>

*/





/*

The Scoped Slots

    What if the parent component needs to access data or methods contained in the child component?

    Let’s say for example that you have a list of fruits (with all the logic handling it) and you want to render them differently depending on the page you’re in.

    First in the parent component --> The fruits Array
fruitsOfTheNinja: [{id: 1, name: '🍋Lemon' }, {id: 2, name: '🥝Kiwi' }, {id: 3, name: '🍑Peach' }, {id: 4, name: '🍌Banana' }, {id: 5, name: '🍎Apple' }]

    The child accessing the fruits Array in the parent component
<Slts :fruits="fruitsOfTheNinja"></Stls>

    In the child component the props gotten from the parent component and a slice method to slice(delete) any fruit 
props: {
  fruits: {
    type: Array,
    required: true,
  }
}, 

methods: {
  slice(id) {
    this.fruits = this.fruits.filter(fruit => fruit.id !== id)
  }
}
  
    child component template 
<template>
	<ul>
		<li v-for="fruit in fruits" :key="fruit.id">
			<slot :fruit="fruit" :slice="slice" />
		</li>
	</ul>
</template>

    Now back to the parent component, the parent component tells the child component which slot it needs AND calls for the props it will use.
<Slts :fruits="fruitsOfTheNinja">
  <template #default="{ fruit, slice }">
    {{ fruit.name }}

    <button @click="slice(fruit.id)">
      ⚔️ Style Slicing
    </button>
  </template> 
</Stls>

    And just like that our parent component can implement its own layout or use methods from the child component. 

*/




/*

    Introducing… 🥁🥁🥁 Dynamic Scoped Slots!
    Let’s say our Chef 👩‍🍳 is creating recipes for the fruits array we used earlier. But he didn’t get enough time to create his recipe for each fruit listed.

    So how do we only show the recipes for only the ones that have been made?
    Namng both slots in the child component, the props and method are the same 
<template>
	<ul>
		<li v-for="fruit in fruits" :key="fruit.id">
			<slot name="fruit" :fruit="fruit" :slice="slice" />
			<slot name="recipe" :fruit="fruit" />
		</li>
	</ul>
</template>

    Only adding one recipe to the fruits Array
{id: 2, name: '🥝Kiwi', recipe: 'Kiwi, Baijiu & Red Date Yoghurt Cocktail 🍸' },
    In the parent component --> the child element, on for the name slot and the other for the recipe slot
<Slts :fruits="fruitsOfTheNinja">
// Default List
  <template #fruit="{ fruit, slice }">
    {{ fruit.name }}
    <button @click="slice(fruit.id)">
      ⚔️ Style Slicing
    </button>
  </template>

  // Adding the Chef Recipes 👩‍🍳
  <template v-if="fruit.recipe" #recipe="{ fruit }">
    {{ fruit.recipe }}
    <video>
      <source src="video_pour_les_fins_gourmets.mp4" />
    </video>
  </template>
</Stls>

*/



export default {
  name: "Slts",
  props: {
    fruits: {
      type: Array,
      required: true,
    }
  }, 

  methods: {
    slice(id) {
      this.fruits = this.fruits.filter(fruit => fruit.id !== id)
    }
  }
}
</script>

<style scoped>
  .child-content {
    background: blue;
  }
</style>