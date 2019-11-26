<template>
  <div id="app" class="small-container">
    <employee-form @add:employee="addEmployee"/>
    <h1>Employees</h1>
    <employee-table  
     :employees="employees"
     @delete:employee="deleteEmployee" 
     @edit:employee="editEmployee"/>
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable.vue'
import EmployeeForm from '@/components/EmployeeForm.vue'
export default {
  name: 'app',
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return{
      employees:[],
    }
  },
  mounted(){
    this.getEmployees()
  },
  methods: {
    async addEmployee(employee) {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users', {
          method: 'POST',
          body: JSON.stringify(employee),
          headers: {'Conten-type': 'application/json; charset=UTF-8'}
        })
        const data = await response.json()
        this.employees = await response.json()
        this.employees = [...this.employees,data]
      } catch (error) {
         console.log(error)
      }
    },
    async deleteEmployee(id){
      try {
        await fetch(`https://jsonplaceholder.typicode.com/users/${id}`,{
          method: "DELETE"
        })
      } catch (error) {
        this.employees = this.employees.filter(employee => employee.id !== id);
      }
    },
    async editEmployee(id, updateEmployee) {
       try {
         const  response = await 
         fetch(`https://jsonplaceholder.typicode.com/users/${id}`,{
           method: 'PUT',
           body : JSON.stringify(updateEmployee),
           headers: {'Content-type': 'application/json; charset=UTF-8'}
         })
        const data = await response.json()
        this.employees = this.employees.map(employee =>(employee.id === id ? data : employee))
        } catch (error) {
         console.log(error)
       }
    },
    async getEmployees() {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users')
        const data = await response.json()
        this.employees = data
      } catch (error) {
        console.log(error)
      }
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
