<template>
  <div class="customer container">
    <!-- 调用组件 -->
    <alert v-if="alert" :message="alert"></alert>
    <h1 class="page-header">用户管理系统</h1>

    <input type="text" class="form-control" placeholder="根据名字进行搜索" v-model="filterInput">


    <table class="table table-stripped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="customer in filterby(customers,filterInput)">
          <td>{{customer.name}}</td>
          <td>{{customer.phone}}</td>
          <td>{{customer.email}}</td>
          <td>
            <router-link class="btn btn-default" :to="'/customer/'+customer.id">详情</router-link>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
    import alert from './alert'
    export default {
        name: 'customer',
        data() {
            return {
                customers: [],
                alert: "",
                filterInput: ""
            }
        },
        methods: {
            fetchcustomers() {
                this.$http.get("http://localhost:3000/users")
                    .then(function(response) {
                        //console.log(response)
                        this.customers = response.body;
                    })
            },
            filterby(customers, value) {
                return customers.filter(function(customer) {
                    return customer.name.match(value);
                })
            }
        },
        created() {
            if (this.$route.query.alert) {
                this.alert = this.$route.query.alert;
            }
            this.fetchcustomers();
        },
        updated() {
            this.fetchcustomers();
        },
        components: {
            alert
        }

    }
</script>


<style scoped>

</style>