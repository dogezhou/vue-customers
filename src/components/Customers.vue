<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">客户管理</h1>
    <input class="form-control" placeholder="输入姓名搜索" v-model="searchQuery">
    <br />
    <table class="table table-striped">
        <thead>
          <tr>
            <th>姓名</th>
            <th>电话</th>
            <th>邮箱</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="customer in filteredCustomers" :key="customer.id">
            <td>{{customer.name}}</td>
            <td>{{customer.phone}}</td>
            <td>{{customer.email}}</td>
            <td><router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">详情</router-link></td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
import Alert from './Alert'

export default {
  name: 'customers',
  data () {
    return {
      customers: [],
      searchQuery: '',
      alert: ''
    }
  },
  methods: {
    fetchCustomers () {
      this.customers = JSON.parse(localStorage.getItem('customers'))
    }
  },
  computed: {
    filteredCustomers () {
      return this.customers.filter((item) => {
        return item.name.indexOf(this.searchQuery) !== -1
      })
    }
  },
  created () {
    if (this.$route.query.alert) {
      this.alert = this.$route.query.alert
    }
    this.fetchCustomers()
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
