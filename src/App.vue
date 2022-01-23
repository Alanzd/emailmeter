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
      let date_to = new Date();
      let date_from = new Date();
      date_from.setMonth(date_from.getMonth()-1);
      usersStats.forEach(userStat => {
        // this.getMonthlySteps(userStat.username);
        
        let user = {
          username : userStat.username,
          monthlySteps: 0,
          weeklySteps: 0,
          dailyAvg: userStat.avg_steps
        }
        this.getWorkouts(userStat.username, date_from, date_to)
            .then(response => {
              user.monthlySteps = this.getMonthlySteps(response.data.results);
              user.weeklySteps = this.getWeeklySteps(response.data.results);
              this.users.push(user);
            })
        });
    },
    async getWorkouts (username, date_from, date_to){
      let response = await axios.get("https://step-meter-pp4publmdq-ez.a.run.app/" + username + "/workouts", {
        headers: {
          'Authorization': 'Token ' + token,
          'Content-Type': 'application/json'
        }, 
        params: {
          'workouts_from': date_from.toISOString().substring(0, 10),
          'workouts_to': date_to.toISOString().substring(0, 10)
        }
      })
      return response
    },

    getMonthlySteps(workouts){
      let steps = 0;
      workouts.forEach(workout => {
        steps += workout.steps;
      })
       return steps;
    },

    getWeeklySteps(workouts){
      let steps = 0;
      var weekAgo = new Date();
      weekAgo.setDate(weekAgo.getDate()-7);
      workouts.forEach(workout => {
        var workoutDate = new Date(workout.date);
        if(workoutDate >= weekAgo){
          steps += workout.steps;
        }      
      })
      return steps;
    }, 
    sortBySelector(selector){
      if(selector === "daily"){
        this.users.sort(function(b, a) {
          return a.dailyAvg - b.dailyAvg;
        });
      }else if(selector === "monthly"){
        this.users.sort(function(b, a) {
          return a.monthlySteps - b.monthlySteps;
        });  
      }else if(selector === "weekly"){
        this.users.sort(function(b, a) {
          return a.weeklySteps - b.weeklySteps;
        });
      }
    }

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
