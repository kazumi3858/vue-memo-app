<template>
  <div class="main-form">
    <div v-show="this.$parent.selectedMemo === 'add-mark'">
      <form @submit.prevent>
        <textarea v-model="newMemo"></textarea>
        <button @click="addMemo">Create</button>
      </form>
    </div>
    <div v-show="typeof this.$parent.selectedMemo === 'object'">
      <form @submit.prevent>
        <textarea></textarea>
        <button>Update</button>
        <button>Delete</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    memos: Array
  },
  data() {
    return {
      newMemo: null
    }
  },
  computed: {
    memoList: function() {
      return this.memos
    }
  },
  methods: {
    // showForm(selectedMemo) {
    //   console.log(selectedMemo)
    // },
    addMemo() {
      if (!this.newMemo) {
        return
      }
      const memoObject = {
        title: this.newMemo.split('\n')[0],
        content: this.newMemo,
        time: Date.now()
      }
      this.memoList.push(memoObject)
      this.newMemo = ''
      this.saveMemos()
    },
    removeMemo(index) {
      this.memoList.splice(index, 1)
      this.saveMemos()
    },
    saveMemos() {
      const jsonMemos = JSON.stringify(this.memoList)
      localStorage.setItem('memos', jsonMemos)
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
