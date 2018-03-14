<template>
  <div class="customers container">
    <h1 class="page-header">客户管理</h1>
    <input class="form-control" placeholder="姓名" v-model="filterInput">
    <br />
    <table class="table table-striped">
        <thead>
          <tr>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Email</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr :key="customer.id" v-for="customer in filterBy(customers, filterInput)">
            <td>{{customer.name}}</td>
            <td>{{customer.phone}}</td>
            <td>{{customer.email}}</td>
            <td><router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">View</router-link></td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'customers',
  data () {
    return {
      customers: [],
      filterInput: ''
    }
  },
  methods: {
    fetchCustomers () {
      this.customers = [
        {
          id: 2,
          name: 'zhou',
          phone: 33333333333,
          email: 'ddd@dddd.com'
        }
      ]
    },
    filterBy (list, value) {
      value = value.charAt(0).toUpperCase() + value.slice(1)
      return list.filter(function (customer) {
        return customer.name.indexOf(value) > -1
      })
    }
  },
  created () {
    this.fetchCustomers()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
