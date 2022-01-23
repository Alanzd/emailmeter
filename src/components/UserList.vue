<template>
  <div class="user-list">
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col"> 
            <button class="btn btn-primary" aria-pressed="true" v-on:click="sortBySelector('monthly')">Monthly step count</button>
          </th>
          <th scope="col"> 
            <button class="btn btn-primary" aria-pressed="true" v-on:click="sortBySelector('weekly')">Weekly step count</button>
          </th>
          <th scope="col"> 
            <button class="btn btn-primary" aria-pressed="true" v-on:click="sortBySelector('daily')">Daily avg</button>
          </th>
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
  methods: {
    sortBySelector(selector){
      this.$parent.sortBySelector(selector);
    }
  },
  props: {
    users: Array
  }
}
</script>