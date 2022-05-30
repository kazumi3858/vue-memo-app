<template>
  <div class="main-form">
    <div v-show="memo.time === null">
      <form @submit.prevent>
        <textarea
          v-model="newMemo"
          class="text-area"
        />
        <div>
          <button
            class="form-button"
            @click="$emit('create-new-memo', newMemo)"
          >
            Create
          </button>
        </div>
      </form>
    </div>
    <div v-show="memo.time !== null && Object.keys(memo).length !== 0">
      <form @submit.prevent>
        <textarea
          v-model="memo.content"
          class="text-area"
        />
        <div>
          <button
            class="form-button"
            @click="$emit('update-memo', memo.content)"
          >
            Update
          </button>
          <button
            class="form-button"
            @click="$emit('destroy-memo')"
          >
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
    selectedMemo: {
      type: Object,
      default: () => {}
    }
  },
  emits: ['select-memo', 'create-new-memo', 'update-memo', 'destroy-memo'],
  data() {
    return {
      newMemo: 'New memo'
    }
  },
  computed: {
    memo() {
      return this.selectedMemo
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
.text-area {
  min-width: 200px;
  width: 400px;
  max-width: 480px;
  height: 400px;
}
.form-button {
  width: 80px;
  color: white;
  background-color: #7d5885;
  border: none;
  border-radius: 8px;
  margin: 8px;
  padding: 8px;
}
.form-button:hover {
  cursor: pointer;
}
</style>
