<template>
  <form @submit.prevent="handleSubmit" class="select-question">
    <dl>
      <dt>{{message}}</dt>
      <dd>
        <select required v-model="selectedValue">
          <template v-for="(choice, i) in choices">
            <option :value="i+1" :key="choice">{{choice}}</option>
          </template>
        </select>
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
export default {
  props: {
    message: String,
    choices: Array,
    value: Number
  },
  data() {
    return {
      selectedValue: this.value
    }
  },
  methods: {
    handleSubmit() {
      this.$emit('input', this.selectedValue)
      this.$emit('next')
    }
  }
}
</script>

<style scoped>
.select-question {
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
