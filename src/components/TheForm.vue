<template>
  <div class="main-form">
    <div v-show="memo.content === null">
      <form @submit.prevent>
        <textarea v-model="newMemo" />
        <div>
          <button @click="create(newMemo)">
            Create
          </button>
        </div>
      </form>
    </div>
    <div v-show="memo.content !== null && Object.keys(memo).length !== 0">
      <form @submit.prevent>
        <textarea v-model="memo.content" />
        <div>
          <button @click="update(memo.content)">
            Update
          </button>
          <button @click="destroy">
            Delete
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    memos: {
      type: Array,
      default: () => []
    },
    selectedMemo: {
      type: Object,
      default: () => {}
    }
  },
  emits: ['select-memo'],
  data() {
    return {
      newMemo: ''
    }
  },
  computed: {
    memoList() {
      return this.memos
    },
    memo: {
      get() {
        return this.selectedMemo
      },
      set(newValue) {
        this.$emit('select-memo', newValue)
      }
    }
  },
  methods: {
    createMemoObject(memoData) {
      return {
        title: memoData.split('\n')[0],
        content: memoData,
        time: Date.now()
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
      this.memo = {}
    },
    destroy() {
      const index = this.memoList.indexOf(this.memo)
      this.memoList.splice(index, 1)
      this.save()
      this.memo = {}
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
.main-form {
  width: 520px;
  padding-top: 40px;
  background-color: white;
  text-align: center;
}
textarea {
  min-width: 200px;
  width: 400px;
  max-width: 480px;
  height: 400px;
}
button {
  width: 80px;
  color: white;
  background-color: #7d5885;
  border: none;
  border-radius: 8px;
  margin: 8px;
  padding: 8px;
}
button:hover {
  cursor: pointer;
}
</style>
