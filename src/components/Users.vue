<template>
  <div class="users">
      <h1>{{ msg }}</h1>

      <form @submit="addUser">
        <input type="text" v-model="newUser.name" placeholder="Enter your name">
        <br>
        <input type="email" v-model="newUser.email" placeholder="Enter your email">
        <br>
        <input type="submit" value="Submit">
      </form>

      <ul>
        <li v-for="user in users" :key="user">
            <input type="checkbox" class="toggle" v-model="user.contacted">
            <span :class="{contacted: user.contacted}">
              {{ user.name }} : {{ user.email }}
              <button v-on:click="deleteUser(user)">X</button>
            </span>
        </li>
      </ul>
  </div>
</template>


<script>
  export default {
    name: 'users',
    props: {
      msg: String,
    },
    data() {
      return {
        newUser: {},
        users: [
            {
              name: "Leanne Graham",
              username: "Bret",
              email: "Sincere@april.biz",
            },
            {
              name: "Ervin Howell",
              username: "Antonette",
              email: "Shanna@melissa.tv",
            },
            {
              name: "Clementine Bauch",
              username: "Samantha",
              email: "Nathan@yesenia.net",
            },
            {
              name: "Patricia Lebsack",
              username: "Karianne",
              email: "Julianne.OConner@kory.org",
            },
        ]
      }
    },

    methods: {
      addUser(e) {
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        })
        e.preventDefault()
      },

      deleteUser(user) {
        this.users.splice(this.users.indexOf(user), 1)
      }
    },

    // created() {
    //    this.$http.get('https://jsonplaceholder.typicode.com/users')
    //       .then(response => this.users = response.data);
    //       // .then(response => console.log(response.json()))
    // }
  }
</script>


<style scoped>
  .contacted {
    text-decoration: line-through;
  }
</style>