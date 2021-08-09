<template>
  <div id="myPlayGround">
    <p>My Favourite Movies</p>

    <ul>
      <li v-for="movie in movies" :key="movie">{{ movie.title }} <button> {{ movie.rate }} </button></li>
    </ul>

    <p> {{ addOn }} </p>
    <p v-html="noteHtml"></p>

    <!-- if the argument of the disabled is true || the button will be disabled -->
    <button @click="changeBk">Background Settings</button>

    <!-- addClass -->
    <br>
    <input type="text" :class="{ red: alert, 'border' : nameAd }">
    <br>
    <input type="text" :class="objRef">
  </div>
</template> 


<script>
   export default {
      name: 'myPlayGround',
      props: {
        changeBk: Function,
      },
      data() {
         return {
            alert: true,      
            nameAd: true,
            note: 'Do not Come Uninvited',
            noteHtml: '<h2> !!Do not Come Uninvited!! </h2>',
            movies: [
              { title: 'Lord of the Rings', rate: 9.1 },
              { title: 'Avengers', rate: 9.3 },
              { title: 'Harry Potter', rate: 9.5 },
              { title: 'Merlin', rate: 9.2 }
            ],
            objRef: {
              red: true,
              border: false,
            }
         }
      },

      computed: {
         addOn() {
            let noteAdd = this.note.split(' ');
            return noteAdd.reverse().join(' ');
         }
      }
   }
</script>


<style scoped>
  li button {
    outline: none;
    border: none;
  }

  .red {
    border: 3px solid red;
  }

  .border {
    background: #696969;
  }
</style>