<template>
  <div class="add container">
    <alert v-if="alert" :message="alert"></alert>
    <h1 class="page-header">编辑用户</h1>
    <form @submit="updatecustomer">
      <div class="well">
        <h4>用户信息</h4>
        <div class="form-group">
          <label>姓名</label>
          <input type="text" class="form-control" placeholder="name" v-model="customer.name">
        </div>

        <div class="form-group">
          <label>电话</label>
          <input type="text" class="form-control" placeholder="phone" v-model="customer.phone">
        </div>
        <div class="form-group">
          <label>邮箱</label>
          <input type="text" class="form-control" placeholder="email" v-model="customer.email">
        </div>
        <div class="form-group">
          <label>学历</label>
          <input type="text" class="form-control" placeholder="education" v-model="customer.education">
        </div>
        <div class="form-group">
          <label>毕业学校</label>
          <input type="text" class="form-control" placeholder="graduationschool" v-model="customer.graduationschool">
        </div>
        <div class="form-group">
          <label>职业</label>
          <input type="text" class="form-control" placeholder="profession" v-model="customer.profession">
        </div>
        <div class="form-group">
          <label>个人简介</label>
          <textarea class="form-control" rows="10" v-model="customer.profile"></textarea>
        </div>
        <button type="submit" class="btn btn-primary">确认</button>
      </div>


    </form>


  </div>
</template>

<script>
    import alert from './alert'
    export default {
        name: 'update',
        data() {
            return {
                customer: {},
                alert: ''
            }
        },
        methods: {
            fetchcustomer(id) {
                this.$http.get("http://localhost:3000/users/" + id)
                    .then(function(response) {
                        this.customer = response.body
                    })
            },
            updatecustomer(e) {
                if (!this.customer.name || !this.customer.phone || !this.customer.email) {
                    //console.log("请添加对应的信息");
                    this.alert = "请添加对应的信息";
                } else {
                    let updatecustomer = {
                        name: this.customer.name,
                        phone: this.customer.phone,
                        email: this.customer.email,
                        education: this.customer.education,
                        graduationschool: this.customer.graduationschool,
                        profession: this.customer.profession,
                        profile: this.customer.profile
                    }
                    this.$http.put("http://localhost:3000/users/" + this.$route.params.id, updatecustomer)
                        .then(function(response) {
                            //console.log(response)
                            // 跳转到主页
                            this.$router.push({
                                path: '/',
                                query: {
                                    alert: "用户信息更新成功!"
                                }
                            });
                        })
                    e.preventDefault();
                }
                e.preventDefault();
            }
        },
        created() {
            this.fetchcustomer(this.$route.params.id);
        },
        component() {
            alert
        }
    }
</script>


<style scoped>

</style>