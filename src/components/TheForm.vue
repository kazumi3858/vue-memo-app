<template>
  <div class="main-form">
    <div v-show="this.memo === 'new-memo'">
      <form @submit.prevent>
        <textarea v-model="newMemo"></textarea>
        <button @click="addMemo(newMemo)">Create</button>
      </form>
    </div>
    <div v-show="typeof this.memo === 'object' && Object.keys(this.memo).length !== 0">
      <form @submit.prevent>
        <textarea v-model="this.memo.content"></textarea>
        <button @click="updateMemo">Update</button>
        <button>Delete</button>
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
      newMemo: null
    }
  },
  computed: {
    memoList: function() {
      return this.memos
    },
    memo: {
      get: function() {
        return this.selectedMemo
      },
      // set: function(value) {
      //   this.$emit('selected-memo', value)
      // }
    }
  },
  methods: {
    // showForm(selectedMemo) {
    //   console.log(selectedMemo)
    // },
    createMemoObject(memoData) {
      return {
        title: memoData.split('\n')[0],
        content: memoData,
        time: Date.now()
      }
    },
    addMemo(memoData) {
      if (!memoData) {
        return
      }
      const memoObject = this.createMemoObject(memoData)
      // {
      //   title: this.newMemo.split('\n')[0],
      //   content: this.newMemo,
      //   time: Date.now()
      // }
      this.memoList.push(memoObject)
      memoData = ''
      this.saveMemos()
    },
    removeMemo(index) {
      this.memoList.splice(index, 1)
      this.saveMemos()
    },
    saveMemos() {
      const jsonMemos = JSON.stringify(this.memoList)
      localStorage.setItem('memos', jsonMemos)
    },
    updateMemo() {
      const index = this.memoList.indexOf(this.memo)
      this.memoList.splice(index, 1)
      this.addMemo(this.memo.content)
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
