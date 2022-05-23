<template>
  <div class="memo-list">
    <h1>memo</h1>
    <span class="create-mark" @click="selectMemo({content: null, formView: true})">+</span>
    <ul>
      <li v-for="memo in memos" :key="memo.time" @click="selectMemo(memo)">
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
    selectMemo(selectedMemo) {
      this.$emit('selected-memo', selectedMemo)
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

li:hover,
.create-mark:hover {
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

.create-mark {
  margin-left: 10px;
  font-size: 30px;
  padding-top: 100px;
}

</style>
