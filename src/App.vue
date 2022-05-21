<template>
  <TheMemoList msg="Memo"/>
  <TheForm/>
</template>

<script>
import TheMemoList from './components/TheMemoList.vue'
import TheForm from './components/TheForm.vue'

export default {
  name: 'App',
  components: {
    TheMemoList,
    TheForm
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
  display: flex;
  justify-content: center;
  height: 100%;
}

body {
  background-color: #c3e0bf;
}
</style>
