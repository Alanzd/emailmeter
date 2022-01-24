<template>
  <div class="user-list">
  <UserDetails/>
    <table class="table table-striped">
      <thead class="thead-dark">
        <tr>
          <th scope="col" class="text-start">Name</th>
          <th scope="col" data-toggle="tooltip" data-placement="top" title="Sort by monthly steps"> 
            <button class="btn btn-block" 
                    v-on:click="sortBySelector('monthly')" 
                    :class="{ 'btn-outline-success': selector != 'monthly', 'btn-success': selector == 'monthly' }">Monthly steps
            </button>
          </th>
          <th scope="col" data-toggle="tooltip" data-placement="top" title="Sort by weekly steps"> 
            <button class="btn btn-block" 
            v-on:click="sortBySelector('weekly')" 
            :class="{ 'btn-outline-success': selector != 'weekly', 'btn-success': selector == 'weekly' }">Weekly steps</button>
          </th>
          <th scope="col" data-toggle="tooltip" data-placement="top" title="Sort by daily average"> 
            <button class="btn btn-block" v-on:click="sortBySelector('daily')" :class="{ 'btn-outline-success': selector != 'daily', 'btn-success': selector == 'daily' }">Daily avg</button>
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
import UserDetails from './UserDetails.vue'

export default {
  name: 'UserList',
  data() {
   return {
    selector: ""
  }
  },
  components: {
    UserRank,
    UserDetails
  },
  methods: {
    sortBySelector(selector){
      this.selector = selector;
      this.$parent.sortBySelector(selector);
    }
  },
  props: {
    users: Array
  }
}
</script>