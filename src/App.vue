<template>
  <Header/>
  <div class="container">
    <div class="row">
      <UserList :users="users"/>
    </div>
  </div> 
</template>

<script>
import Header from './components/Header.vue'
import UserList from './components/UserList.vue'
import axios from 'axios'

let token = "af61aed7399dc6a636e443cdc8a2d55db97c524a"

export default {
  name: 'App',
  data () {
    return {
      users: []
    }
  },
  methods: {
    getUsers(url) {
      axios.get(url, {
        headers: {
          'Authorization': 'Token ' + token,
          'Content-Type': 'application/json'
        }
      })
      .then(response => {
        let usersStats = response.data.results;
        this.composeRanks(usersStats);
        let next = response.data.next;
        if(next){
          this.getUsers(next);
        }
      })

    },
    composeRanks (usersStats) {
      usersStats.forEach(userStat => {
        // this.getMonthlySteps(userStat.username);
        this.users.push({
          username : userStat.username,
          monthlySteps: 55,
          weeklySteps: 40,
          dailyAvg: userStat.avg_steps
        })   
      })
    },
    // getMonthlySteps (username){
    //   axios.get("https://step-meter-pp4publmdq-ez.a.run.app/" + username + "/workouts", {
    //     headers: {
    //       'Authorization': 'Token ' + token,
    //       'Content-Type': 'application/json'
    //     }
    //   })
    //   .then(response => {
    //     let usersWorkouts = response.data.results;
    //     let steps ;
    //     usersWorkouts.forEach(workout=> {
    //       if(workout.date)
    //       steps += workout. 
  
    //     });
    //   })
    // }
  },
  mounted() {
    this.getUsers("https://step-meter-pp4publmdq-ez.a.run.app/users");
  },
  components: {
    Header,
    UserList,
  }
}
</script>

<style>
#emailmeter {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
