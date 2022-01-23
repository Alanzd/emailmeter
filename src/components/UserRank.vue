<template>
    <tr>
      <th scope="row">{{ index }}</th>
      <td>{{ user.username }}</td>
      <td>{{ user.monthlySteps }}</td>
      <td>{{ user.weeklySteps }}</td>
      <td>{{ user.dailyAvg }}</td>
    </tr>  
</template>

<script>
export default {
  name: 'UserRank',
  props: {
    index: Number,
    user: Object,
  }
}
</script>


