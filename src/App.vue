<template>
  <the-memo-list :memos="memos" @send-selected-memo-data="checkSelectedMemo"/>
  <the-form :memos="memos" :selectedMemo="selectedMemo"/>
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
      selectedMemo: null
      // newMemo: null
    }
  },
  mounted() {
    if (localStorage.getItem('memos')) {
      try {
        this.memos = JSON.parse(localStorage.getItem('memos'));
      } catch (e) {
        localStorage.removeItem('memos');
      }
    }
  },
  methods: {
    checkSelectedMemo(selectedMemo) {
      this.selectedMemo = selectedMemo
      // this.$refs.form.showForm(this.selectedMemo)
    }
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
