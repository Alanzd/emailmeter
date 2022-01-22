<template>
<div class="row title align-items-center">
  <div class="col-6 ml ">
    <h1 class="px-2 text-start">Email meter</h1>
  </div>
  <div class="col-6">
    <h1 class=" px-2 text-end">{{date}}</h1>
  </div>
</div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      date: (new Date()).toLocaleDateString()
    }
    
  }
}
</script>
