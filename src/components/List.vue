<template>
  <div class="container">
    <p class="border border-info"> 狀態: {{ status }} </p>
    <div class="form-inline">
      <input type="text" class="form-control mr-2" v-model="username">
      <button type="button" class="btn btn-primary" @click="changeName">更新姓名</button>
    </div>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>#</th>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Username</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,i) in listData" >
          <th scope="row" class="p-4">{{i+1}}</th>
          <td><img :src="item.picture.thumbnail" alt=""></td>
          <td class="p-4">{{item.name.first}}</td>
          <td class="p-4">{{item.name.last}}</td>
          <td class="p-4">{{item.email}}</td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  name: 'List',
  props: ["status"],
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      listData: "",
      username: "Max"
    }
  },
  methods: {
    getData() {
      let vm = this
      vm.axios.get("https://randomuser.me/api/?results=50")
        .then(function(response) {
          // console.log(response)
          console.log(response.data)
          vm.listData = response.data.results
        })
        .catch(function(error) {
          console.log(error)
        })
    },
    changeName(){
      let vm=this
      vm.$emit("pushNewName",vm.username)
      vm.username=""
    }
  },
  mounted() {
    this.getData()
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
