<template>
  <div class="user-list">
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Monthly step count</th>
          <th scope="col">Weekly step count</th>
          <th scope="col">Daily avg</th>
        </tr>
      </thead>
      <tbody>
       <UserRank v-for="(user, index) in users" :key="index" :index="index+1" :user="user"/>
      </tbody>
    </table>   
  </div>
</template>

<script>
import UserRank from './UserRank.vue'

export default {
  name: 'UserList',
  components: {
    UserRank
  },
  props: {
    users: Array
  }
}
</script>