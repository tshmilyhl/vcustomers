<template>
 <div class="customers container">
   <alert :message="alert"></alert>
   <h1 class="page-header">用户管理系统</h1>
<!--   搜索功能-->
   <input type="text"class="form-control" placeholder="搜索" v-model="filterInput">
   <br/>
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
     <tr v-for="customer in filterBy(customers,filterInput) ">
       <td >{{customer.name}}</td>
       <td>{{customer.phone}}</td>
       <td>{{customer.email}}</td>
       <td>
         <router-link class="btn btn-default" :to="'/customer/'+customer.id">详情</router-link>
       </td>
       <td></td>
     </tr>
     </tbody>
   </table>
 </div>
</template>

<script>
import Alert from "./Alert";
export default {
  name: 'Customers',
  components:{
    Alert
  },
  data () {
    return {
      customers:[],
      alert:"",
      filterInput:""
    }
  },
  created(){
    if(this.$route.query.alert){
      this.alert = this.$route.query.alert
    }
    this.fetchCustomers()
  },
  updated(){
    this.fetchCustomers()
  },
  methods:{
    fetchCustomers(){
      this.$http.get("http://localhost:3000/users")
      .then(res=>{
         console.log(res)
        this.customers = res.data
      })
    },
    filterBy(customers,value){
      return customers.filter(function(customer){
        if(customer.name !==undefined){
          return customer.name.match(value)
        }

       // return  customer.name.indexOf(value) && (customer.name!==undefined)
      })
    }
    // filterBy(customers,value){
    //   return customers.filter(customer=>{
    //     console.log(customer.name.indexOf(value))
    //   return customer.name.indexOf(value)
    //   })
    // }
  }
}
</script>

</style>
