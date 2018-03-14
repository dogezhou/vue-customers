<template>
  <div class="details container">
    <router-link to="/">返回</router-link>
    <h1 class="page-header">{{customer.name}}
      <span class="pull-right">
        <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">编辑</router-link>
        <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item"><span class="glyphicon glyphicon-phone" aria-hidden="true"></span> {{customer.phone}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span> {{customer.email}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
      customer: ''
    }
  },
  methods: {
    fetchCustomer (id) {
      let customers = JSON.parse(localStorage.getItem('customers'))
      customers.forEach(element => {
        console.log('element', element)
        if (element.id === Number(id)) {
          this.customer = element
        }
      })
    },
    deleteCustomer (id) {
      let customers = JSON.parse(localStorage.getItem('customers'))
      customers.forEach((element, index) => {
        if (element.id === Number(id)) {
          customers.splice(index, index + 1)
        }
      })
      localStorage.setItem('customers', JSON.stringify(customers))
      this.$router.push({
        path: '/',
        query: { alert: '用户删除' }
      })
    }
  },
  created () {
    this.fetchCustomer(this.$route.params.id)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
