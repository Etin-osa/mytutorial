<template>
  <div class="filters">
    <div class="filters">
      <h1>Hi {{ name | capitalize | prepend('Mr') }} </h1>
    </div>
  </div>
</template>

<script>
/*

    In Vue components, filters are functionalities that allow us to obtain different formats in the output of the dynamic data of its state. That is, they do not change the data of a component, they can only format their data in rendering.

    Filters are a functionality provided by Vue components that let you apply formatting and transformations to any part of your template dynamic data, they don't change a component data or anything, but they only affect the output


Basic Examples
    <div class="filters">
      <h1>Hi {{ name }}</h1>
    </div>

    return {
      name: 'Flavio',
    }

    What if you want to check that name actually contains a value, and if not, print 'there' so that our template will print 'Hi there', in order for that to happen the fallback filter function is created below

    filters: {
      fallback(name) {
        return name ? name : 'there' ;
      }
    }

    To add it to the DOM in order to be printed
    <h1>Hi {{ name | fallback }}</h1>

    Notice the syntax to apply a filter, which is '| filterName'. If you’re familiar with Unix, that’s the Unix pipe operator, which is used to pass the output of an operation as an input to the next one.

    The filters property of the component is an object. A single filter is a function that accepts a value and returns another value.

    The returned value is the one that’s actually printed in the Vue.js template.

    The filter, of course, has access to the component data and methods.

    What’s a good use case for filters?

    transforming a string, for example, capitalizing or making it lowercase
    formatting a price
    Above you saw a simple example of a filter: {{ name | fallback }}.

    Filters can be chained, by repeating the pipe syntax:
    {{ name | fallback | capitalize }}
    This first applies the fallback filter, then the capitalize filter.

    capitalize(name) {
      return name[0].toUpperCase() + name.slice(1)
    }


Advanced filters can also accept parameters, using the normal function parameters syntax:
    <h1>Hi {{ name | prepend('The') }}</h1>

    prepend: (name, prefix) => {
      return `${prefix}, ${name}`
    }

NOTE: it dosen't have to be an arrow function, it could have been written like this 
    prepend (name, prefix) {
      return `${prefix}, ${name}`
    }, And have the same result
    The reason for using it here will be explained

    If you pass parameters to a filter, the first one passed to the filter function is always the item in the template interpolation (name in this case), followed by the explicit parameters you passed.

    You can use multiple parameters by separating them using a comma.

    Notice I used an arrow function. We avoid arrow function in methods and computed properties generally because they almost always reference this to access the component data, but in this case, the filter does not need to access this but receives all the data it needs through the parameters, and we can safely use the simpler arrow function syntax.
*/









/*

Local filters

    According to the official documentation, the use of filters occurs within mustache interpolations and v-bind expressions. See an example of the formatting of the filter in the template:

    <!-- in interpolations text --> 
    {{ message | capitalize }}  

    <!-- in attribute interconnections --> 
    <div v-bind:text="message | capitalize"></div>

    Local filters are created in the vue file they are used like the examples above in the basic examples

Global Filters
    There are certain situations where a particular filter can be used on several components within your application, especially in those larger projects, where several interactions of the system can occur throughout the project.
    For this, there is the possibility of creating global filters, and just as I said earlier, equally to mixins, plugins, among others, they are available anywhere in your project, facilitating their use and the reuse of codes.

    Vue.filter('capitalize', value => value[0].toUpperCase() + value.slice(1))

    Created in the main.js file

    In this example, we see the creation of a global filter, using the .filter property inside the main.js. If your application uses many filters, for organization reasons, it is recommended to create a separate file and import the Vue into your filter 'filter.js' file and place all filters there and import them into the main.js file. And there is a detail that is very important and should always be remembered: when a global filter has the same name as a local filter, the local filter will have priority.

*/


export default {
  name: 'filters',
  data() {
    return {
      name: 'etinosa',
    }
  },

  filters: {
    fallback(name) {
      return name ? name : 'There' ;
    },

    prepend: (name, prefix) => {
      return `${prefix}. ${name}`
    }
  }
}
</script>

<style>

</style>