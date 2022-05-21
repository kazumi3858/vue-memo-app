<template>
  <div class="main-form">
    <form>
      <textarea></textarea>
      <button>Create</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'TheForm',
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

.main-form {
  width: 400px;
  background-color: gray;
}

textarea {
  width: 300px;
  height: 200px;
}
</style>

