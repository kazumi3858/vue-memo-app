<template>
  <div class="memo-list">
    <h1 class="app-title">
      memo
    </h1>
    <span
      class="create-mark"
      @click="select({time: null})"
    >+</span>
    <ul class="lists">
      <li
        v-for="memo in memos"
        :key="memo.time"
        class="each-list"
      >
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
    memos: {
      type: Array,
      default: () => []
    }
  },
  emits: ['select-memo'],
  methods: {
    select(selectedMemo) {
      this.$emit('select-memo', selectedMemo)
    }
  }
}
</script>

<style scoped>
.app-title {
  display: inline-block;
}
.lists {
  list-style-type: none;
  padding: 0;
}
.each-list {
  margin-bottom: 16px;
}
.each-list:hover,
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
