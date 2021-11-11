<template>
 <div class="customers container">
   <h1 class="page-header">用户管理系统</h1>
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
     <tr v-for="customer in customers">
       <td >{{customer.name}}</td>
       <td>{{customer.phone}}</td>
       <td>{{customer.email}}</td>
       <td></td>
     </tr>
     </tbody>
   </table>
 </div>
</template>

<script>
export default {
  name: 'Customers',
  data () {
    return {
  customers:[]
    }
  },
  created(){
    this.fetchCustomers()
  },
  methods:{
    fetchCustomers(){
      this.$http.get("http://localhost:3000/users")
      .then(res=>{
        console.log(res)
        this.customers = res.data
      })
    }
  }
}
</script>

</style>
