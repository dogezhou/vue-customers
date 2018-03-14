<template>
  <div class="edit container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">编辑用户</h1>
    <form v-on:submit="updateCustomer">
        <div class="well">
            <h4>用户信息</h4>
            <div class="form-group">
                <label>姓名</label>
                <input type="text" class="form-control" placeholder="姓名" v-model="customer.name">
            </div>
        </div>
        <div class="well">
            <h4>联系方式</h4>
            <div class="form-group">
                <label>Email</label>
                <input type="text" class="form-control" placeholder="Email" v-model="customer.email">
            </div>
            <div class="form-group">
                <label>Phone</label>
                <input type="text" class="form-control" placeholder="Phone" v-model="customer.phone">
            </div>
        </div>
        <button type="submit" class="btn btn-primary">提交</button>
    </form>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'add',
  data () {
    return {
      customer: {},
      alert: ''
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
    updateCustomer (e) {
      if (
        !this.customer.name ||
        !this.customer.phone ||
        !this.customer.email
      ) {
        this.alert = '请填写全部内容'
      } else {
        let updCustomer = Object.assign(this.customer, {
          name: this.customer.name,
          phone: this.customer.phone,
          email: this.customer.email
        })
        var customers = JSON.parse(localStorage.getItem('customers'))
        customers.forEach((element, index) => {
          if (element.id === this.customer.id) {
            customers.splice(index, index + 1)
          }
        })
        customers.push(updCustomer)
        localStorage.setItem('customers', JSON.stringify(customers))
        this.$router.push({
          path: '/',
          query: { alert: '用户修改成功！' }
        })
        e.preventDefault()
      }
      e.preventDefault()
    }
  },
  created () {
    this.fetchCustomer(this.$route.params.id)
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
