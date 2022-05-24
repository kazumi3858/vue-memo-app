<template>
  <div class="main-content">
    <the-memo-list :memos="memos" @select-memo="checkSelectedMemo" />
    <the-form :memos="memos" :selected-memo="selectedMemo" @select-memo="checkSelectedMemo" />
  </div>
</template>

<script>
import TheMemoList from './components/TheMemoList.vue'
import TheForm from './components/TheForm.vue'

export default {
  components: {
    TheMemoList,
    TheForm
  },
  data() {
    return {
      memos: [],
      selectedMemo: {}
    }
  },
  mounted() {
    if (localStorage.getItem('memos')) {
      try {
        this.memos = JSON.parse(localStorage.getItem('memos'))
      } catch (e) {
        localStorage.removeItem('memos')
      }
    }
  },
  methods: {
    checkSelectedMemo(selectedMemo) {
      this.selectedMemo = selectedMemo
    }
  }
}
</script>

<style>
html,
#app {
  height: 100%;
  min-height: 500px;
}
body {
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: #ccc0d1;
}
.main-content {
  display: flex;
  justify-content: center;
  height: 100%;
}
</style>
