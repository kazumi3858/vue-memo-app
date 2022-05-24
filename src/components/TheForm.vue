<template>
  <div class="main-form">
    <div v-show="memo.content === null && memo.formView">
      <form @submit.prevent>
        <textarea v-model="newMemo"></textarea>
        <button @click="create(newMemo)">Create</button>
      </form>
    </div>
    <div v-show="memo.content !== null && Object.keys(memo).length !== 0 && memo.formView">
      <form @submit.prevent>
        <textarea v-model="memo.content"></textarea>
        <button @click="update(memo.content)">Update</button>
        <button @click="destroy">Delete</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    memos: Array,
    selectedMemo: [Object, String]
  },
  data() {
    return {
      newMemo: ''
    }
  },
  computed: {
    memoList() {
      return this.memos
    },
    memo() {
      return this.selectedMemo
    }
  },
  methods: {
    createMemoObject(memoData) {
      return {
        title: memoData.split('\n')[0],
        content: memoData,
        time: Date.now(),
        formView: true
      }
    },
    create(memoData) {
      this.addMemoToList(memoData)
      this.newMemo = ''
    },
    addMemoToList(memoData) {
      if (!memoData) {
        return
      }
      this.memoList.push(this.createMemoObject(memoData))
      this.save()
      this.memo.formView = false
    },
    destroy() {
      const index = this.memoList.indexOf(this.memo)
      this.memoList.splice(index, 1)
      this.save()
      this.memo.formView = false
    },
    save() {
      const jsonMemos = JSON.stringify(this.memoList)
      localStorage.setItem('memos', jsonMemos)
    },
    update(memoData) {
      const index = this.memoList.indexOf(this.memo)
      this.memoList.splice(index, 1)
      this.addMemoToList(memoData)
    }
  }
}

</script>

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
