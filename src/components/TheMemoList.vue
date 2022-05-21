<template>
  <div class="memo-list">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'TheMemoList',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.memo-list {
  width: 400px;
  background-color: pink;
}
</style>
