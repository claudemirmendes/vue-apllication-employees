<template>
  <div id="app" class="small-container">
    <employee-form> </employee-form>
    <h1>Employees</h1>
    <employee-table  :employees="employees"> </employee-table>
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
      employees:[
        {
        id:1,
        name: 'Richard',
        email: 'richard@geq.com.br',
        },
        {
          id:2,
          name: 'nome de teste',
          email: 'emailteste@geq.com.br'
        },
        {
          id : 3,
          name : 'Dinesh',
          email: 'dinesh@geq.com.br'  
        }
      ]
    }
  }
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
