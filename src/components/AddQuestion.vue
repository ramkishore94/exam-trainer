<template>
  <div class="container">
    <div v-if="isEditorMode == false" class="container">
      <div class="row">
        <textarea v-model="question_input" class="question_input h4 border border-2"></textarea>
      </div>
      <div class="row">
        <textarea v-model="options_input" class="options_input h5 border border-2"></textarea>
      </div>
      <div class="row">
       <button @click="submit()" class="btn btn-primary">Submit</button>
      </div>
    </div>
    <div v-else-if="isEditorMode" class="container">
      <div class="h1">This is editor mode.</div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      isEditorMode: false,
      question_input: '',
      options_input: '',
      question: {
        body: '',
        options: []
      }
    }
  },
  methods: {
    optionsManipulator () {
      return new Promise((resolve, reject) => {
        let ufOptions = this.options_input
        const options = []
        ufOptions = ufOptions.split('\n')
        ufOptions.forEach((option, index) => {
          options.push({
            id: index,
            body: option
          })
        })
        if (options.length > 0 && this.question_input.length > 0) {
          resolve(options)
        } else reject(new Error('input question or options manipulation failed'))
      })
    },
    async submit () {
      try {
        this.question.options = await this.optionsManipulator()
        this.question.body = this.question_input
        this.isEditorMode = true
        console.log(this.question.body)
        console.log(this.question.options)
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<style scoped>
  .question_input{
    height: 30vh;
  }
  .options_input{
    height: 20vh;
  }
</style>
