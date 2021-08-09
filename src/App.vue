<template>
  <div id="app" class="small-container">
<!--     
    <div class="gridHead">
      <div class="gridChild grid1">
        <Users msg="Hello Vue!!" />
      </div>
      <div class="gridChild grid2">
        <Play 
          :changeBk="backColor"  
        />
      </div>
      <div class="gridChild grid3">
        <Test 
          :borderArea="borderArea"
        />
      </div>
    </div> 
-->

    <!-- Deep dive into Vue js -->
    <h1>Employees</h1>

    <employee-form @add:employee="addEmployee" />
    <employee-table 
      :employees="employees" 
      @del-employee="deleteEmployee" 
      @edit-employee="editEmployee"
    /> 


    <!-- Watcher 
    <watcher /> -->


    <!-- Computed property
    <Computed /> -->


    <!-- Filters 
    <Filters /> -->

    <!-- Slots 
    <h2>Parent</h2>
    <Slts :fruits="fruitsOfTheNinja">
      <template #fruit="{ fruit, slice }">
        {{ fruit.name }}

        <button v-on:click="slice(fruit.id)">
          ⚔️ Style Slicing
        </button>
      </template>

      <template #recipe="{ fruit }">
        <span v-if="fruit.recipe">
          {{ fruit.recipe }}
        </span>
      </template>
    </Slts> -->
  </div>
</template>

<script>
// import Test from './components/Test'
// import Play from './components/Play'
// import Users from './components/Users'

// Deep dive into Vue js 
import EmployeeTable from './components/EmployeeTable'
import EmployeeForm from './components/EmployeeForm'


// Watcher
/* import Watcher from './components/Watcher' */


// Computed property
// import Computed from './components/Computed'


// Filter
// import Filters from './components/Filters'


// Slots
/* import Slts from './components/Slts' */


  export default {
    name: 'App',
    components: {
      // Test, 
      // Play,
      // Users

      // Deep dive into Vue js 
      EmployeeTable,
      EmployeeForm, 
      
      // Watcher
      /* Watcher, */ 

      // Computed property
      // Computed


      // Filters
      // Filters 

      // Slots
      /* Slts */
    }, 
    
    data() {
      return {
        Mark: 'pretend to be something important',
        // Deep dive into Vue js
        backConscience: false,
        employees: [
          {
            id: 1,
            name: 'Richard Hendricks',
            email: 'richard@piedpiper.com',
          },
          {
            id: 2,
            name: 'Bertram Gilfoyle',
            email: 'gilfoyle@piedpiper.com',
          },
          {
            id: 3,
            name: 'Dinesh Chugtai',
            email: 'dinesh@piedpiper.com',
          },
        ],

        //End of deep dive in data

      // Slts
        fruitsOfTheNinja: [
          {
            id: 1,
            name: '🍋Lemon'
          },
          {
            id: 2,
            name: '🥝Kiwi',
            recipe: 'Kiwi, Baijiu & Red Date Yoghurt Cocktail 🍸'
          },
          {
            id: 3,
            name: '🍑Peach'
          },
          {
            id: 4,
            name: '🍌Banana'
          },
          {
            id: 5,
            name: '🍎Apple'
          }
			  ]
      }
    },
    
    methods: {
      backColor() {
        const bk = document.querySelector('#app');

        if (!this.backConscience) {
          bk.style.backgroundColor = 'blueviolet'; 
          this.backConscience = true;
        } else {
          bk.style.backgroundColor = '#fff'; 
          this.backConscience = false;
        }
      },

      borderArea() {
        const bk = document.querySelector('#app');

        if (bk.style.backgroundColor === 'blueviolet') {
          bk.style.border = '1px solid black'
          bk.style.borderRadius = '8px'
        } else {
          bk.style.border = 'none'
          bk.style.borderRadius = 'none';
        }
      },


      // Deep dive into Vue js 
      async getEmployees() {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users')
          const data = await response.json()
          this.employees = data
        } catch(error) {
          console.error(error)
        }
      },

      async addEmployee(employee) {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users', {
            method: 'POST',
            body: JSON.stringify(employee),
            headers: { 'Content-type': 'application/json; charset=UTF-8' },
          })
          const data = await response.json();
          this.employees = [...this.employees, data];
        } catch (error) {
          console.log(error);
        }
      },

      /* 'normal addEmployee function without fetching data from an API' 
          addEmployee(employee) {
            const lastID = this.employees.length > 0 ? this.employees[this.employees.length - 1].id : 0;
            const id = lastID + 1
            const newEmployee = { ...employee, id}
            this.employees = [...this.employees, newEmployee]
          } 
      */

      async deleteEmployee(id) {
        try {
          await fetch(`https://jsonplaceholder.typicode.com/users${id}`, {
            method: 'DELETE',
          })
          this.employees = this.employees.filter(employee => employee.id !== id)
        } catch(error) {
          console.error(error)
        }
      },
      /*deleteEmployee(id) {
        this.employees = this.employees.filter(employee => employee.id !== id)
      },*/

      async editEmployee(id, updateEmployee) {
        try {
          const response = await fetch(`https://jsonplaceholder.typicode.com/users${id}`, {
            method: 'PUT',
            body: JSON.stringify(updateEmployee),
            headers: { 'Content-type': 'application/json; charset=UTF-8' },
          })

          const data = await response.json()
          this.employees = this.employees.map(employee => employee.id === id ? data : employee)
        } catch(error) {
          console.error(error)
        }
      }
      /*editEmployee(id, updateEmployee) {
        this.employees = this.employees.map(employee => employee.id === id ? updateEmployee : employee)
      },*/

    },

    mounted () {
      this.getEmployees()
    }
    //End of deep dive in script

  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin: 30px 50px;
  }

  .gridHead {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  .gridChild {
    margin: 0 auto;
  }

  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }


  input:active,
  input:focus,
  input:checked,
  button:active,
  button:focus,
  button:checked {
    outline: none;
  }
</style>
