<template>
  <div class="details container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
      {{customer.name}}
      <span class="pull-right">
        <router-link class="btn btn-primary" :to="'/edit/'+customer.id">编辑</router-link>
        <button class="btn btn-danger" @click="deletecustomer(customer.id)">
          删除
        </button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item"><span>{{customer.phone}}</span></li>
    </ul>

    <ul class="list-group">
      <li class="list-group-item"><span>{{customer.email}}</span></li>
    </ul>

    <ul class="list-group">
      <li class="list-group-item"><span>{{customer.education}}</span></li>
    </ul>

    <ul class="list-group">
      <li class="list-group-item"><span>{{customer.graduationschool}}</span></li>
    </ul>

    <ul class="list-group">
      <li class="list-group-item"><span>{{customer.profession}}</span></li>
    </ul>

    <ul class="list-group">
      <li class="list-group-item"><span>{{customer.profile}}</span></li>
    </ul>

  </div>
</template>

<script>
    export default {
        name: 'customerdetails',
        data() {
            return {
                customer: "",

            }
        },
        methods: {
            // 获取用户数据
            fetchcustomers(id) {
                this.$http.get("http://localhost:3000/users/" + id)
                    .then(function(response) {
                        //console.log(response)
                        this.customer = response.body;
                    })
            },
            // 删除数据
            deletecustomer(id) {
                //console.log(id)
                this.$http.delete("http://localhost:3000/users/" + id)
                    .then(function(response) {
                        this.$router.push({
                            path: "/",
                            query: {
                                alert: "用户删除成功!"
                            }
                        })
                    })
            }
        },
        created() {
            this.fetchcustomers(this.$route.params.id);
        }
    }
</script>


<style scoped>

</style>