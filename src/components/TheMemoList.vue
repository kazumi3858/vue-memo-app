<template>
  <div class="memo-list">
    <h1>memo</h1>
    <span class="add-mark" @click="selectFromList('add-mark')">+</span>
    <ul>
      <li v-for="memo in memos" :key="memo.time" @click="selectFromList(memo)">
      {{ memo.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    memos: Array
  },
  methods: {
    selectFromList (selectedMemo) {
      this.$emit('send-selected-memo-data', selectedMemo)
    }
  }
}
</script>

<style scoped>
h1 {
  display: inline-block;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 0 10px;
}

li:hover, .add-mark:hover {
  color: blue;
  cursor: pointer;
}

a {
  color: #42b983;
}

.memo-list {
  width: 400px;
  background-color: pink;
}

.add-mark {
  margin-left: 10px;
  font-size: 30px;
  padding-top: 100px;
}
</style>
