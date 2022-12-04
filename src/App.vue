<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <employee-form @add:employee="addEmployee" />
    <!-- v-bind -->
    <employee-table 
    :employees="employees" 
    @delete:employee="deleteEmployee"
    @edit:employee="editEmployee" />
  </div>
</template>

<script>
// Import components
import EmployeeTable from '@/components/EmployeeTable.vue'
import EmployeeForm from '@/components/EmployeeForm.vue';

  export default {
    name: 'app',
    components: {
      EmployeeTable,
      EmployeeForm,
  },
  data() {
    return {
      employees: [
          {
            id: 1,
            name: 'Chabs Kim',
            email: 'chaba@chabs.com',
          },
            {
            id: 2,
            name: 'Chris Kim',
            email: 'hooman@chabs.com',
          },
          {
            id: 3,
            name: 'Sangba Chabs',
            email: 'hooman2@chabs.com',
          },
        ],
      }
  },
  methods: {
    addEmployee(employee) {
        const lastId =
          this.employees.length > 0
            ? this.employees[this.employees.length - 1].id
            : 0;
        const id = lastId + 1;
        const newEmployee = { ...employee, id };

        this.employees = [...this.employees, newEmployee];
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter(
          employee => employee.id !== id
        )
    },
    editEmployee(id, updatedEmployee) {
      this.employees = this.employees.map(employee =>
          employee.id === id
            ? updatedEmployee
            : employee
        )
      }
    }
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>