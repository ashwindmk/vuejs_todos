<template>
  <div class="hello">
    <h3> {{msg}} </h3>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<style scoped>
.hello {
  text-align: center;
}

h3 {
  margin: 20px 0;
}
</style>
