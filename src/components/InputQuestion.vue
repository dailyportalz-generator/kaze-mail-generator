<template>
  <form @submit.prevent="handleSubmit" class="input-question">
    <dl>
      <dt>まず、相手の名前と敬称を入れてください。</dt>
      <dd>
        <input type="text" required v-model="name">
        <select required v-model="title">
          <option :value="1">さま</option>
          <option :value="2">様</option>
          <option :value="3">殿</option>
          <option :value="4">さん</option>
          <option :value="5">くん</option>
          <option :value="6">ちゃん</option>
        </select>
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      title: 1,
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('start', { name: this.name, title: this.title })
    }
  }
}
</script>

<style scoped>
.input-question {
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: dotted 1px #c6c6c6;
}

h3 {
  font-size: 1em;
}

dd {
  margin: 16px 0 0;
  padding: 0 0 8px 0;
}

button {
  width: 60px;
}

input[type='text'] {
  margin-right: 20px;
}
</style>
