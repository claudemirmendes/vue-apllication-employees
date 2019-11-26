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
  methods: {
    addEmployee(employee) {
      const  lastId = this.employees.length > 0 
      ? this.employees[this.employees.length - 1 ].id
      : 0;
      const id  = lastId + 1;
      const newEmployee = {...employee, id};

      this.employees = [...this.employees, newEmployee]
    },
    deleteEmployee(id){
      this.employees = this.employees.filter(
        employee => employee.id !== id
      )
    },
    editEmployee(id, updateEmployee) {
      this.employees = this.employees.map(employee =>
        employee.id === id ? updateEmployee : employee
      )
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
