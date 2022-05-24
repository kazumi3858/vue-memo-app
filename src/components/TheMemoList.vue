<template>
  <div class="memo-list">
    <h1>memo</h1>
    <span class="create-mark" @click="select({content: null})">+</span>
    <ul>
      <li v-for="memo in memos" :key="memo.time">
        <div @click="select(memo)">
          {{ memo.title }}
        </div>
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
    select(selectedMemo) {
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
  margin-bottom: 16px;
}

li:hover,
.create-mark:hover {
  color: #91377c;
  cursor: pointer;
}

.memo-list {
  width: 400px;
  padding: 16px 16px 16px 40px;
  background-color: white;
}

.create-mark {
  margin-left: 8px;
  font-size: 30px;
  color: gray;
}

</style>
