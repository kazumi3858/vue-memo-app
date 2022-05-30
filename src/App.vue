<template>
  <div class="main-content">
    <memo-list
      :memos="memos"
      @select-memo="checkSelectedMemo"
    />
    <the-form
      :selected-memo="selectedMemo"
      @create-new-memo="create"
      @update-memo="update"
      @destroy-memo="destroy"
    />
  </div>
</template>

<script>
import MemoList from './components/MemoList.vue'
import TheForm from './components/TheForm.vue'

export default {
  components: {
    MemoList,
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
    },
    createMemoObject(memoData) {
      return {
        title: memoData.split('\n')[0],
        content: memoData,
        time: Date.now()
      }
    },
    create(memoData) {
      console.log(memoData)
      this.addMemoToList(memoData)
      this.newMemo = 'New memo'
    },
    addMemoToList(memoData) {
      if (!memoData) {
        return
      }
      this.memos.push(this.createMemoObject(memoData))
      this.save()
      this.selectedMemo = {}
    },
    destroy() {
      const index = this.memos.indexOf(this.selectedMemo)
      this.memos.splice(index, 1)
      this.save()
      this.selectedMemo = {}
    },
    save() {
      const jsonMemos = JSON.stringify(this.memos)
      localStorage.setItem('memos', jsonMemos)
    },
    update(memoData) {
      const index = this.memos.indexOf(this.selectedMemo)
      this.memos.splice(index, 1)
      this.addMemoToList(memoData)
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
