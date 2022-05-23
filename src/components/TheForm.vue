<template>
  <div class="main-form">
    <div v-show="memo.content === null && memo.formView">
      <form @submit.prevent>
        <textarea v-model="newMemo"></textarea>
        <button @click="addMemo(newMemo)">Create</button>
      </form>
    </div>
    <div v-show="memo.content !== null && Object.keys(memo).length !== 0 && memo.formView">
      <form @submit.prevent>
        <textarea v-model="memo.content"></textarea>
        <button @click="updateMemo(memo.content)">Update</button>
        <button @click="deleteMemo">Delete</button>
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
    memoList: function() {
      return this.memos
    },
    memo: {
      get: function() {
        return this.selectedMemo
      }
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
    addMemo(data) {
      this.updateList(data)
      this.newMemo = ''
    },
    updateList(data) {
      if (!data) {
        return
      }
      const memoObject = this.createMemoObject(data)
      this.memoList.push(memoObject)
      this.saveMemos()
      this.memo.formView = false
    },
    deleteMemo() {
      const index = this.memoList.indexOf(this.memo)
      this.memoList.splice(index, 1)
      this.saveMemos()
      this.memo.formView = false
    },
    saveMemos() {
      const jsonMemos = JSON.stringify(this.memoList)
      localStorage.setItem('memos', jsonMemos)
    },
    updateMemo(data) {
      const index = this.memoList.indexOf(this.memo)
      this.memoList.splice(index, 1)
      this.updateList(data)
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
