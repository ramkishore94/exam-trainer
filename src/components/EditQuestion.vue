<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <div class="row">
          <h3 class="card-title">
            {{ question.body }}
          </h3>
        </div>
        <div class="row">
          <ul class="list-group list-group-flush">
            <li v-for="option in question.options" :key="option.id" class="list-group-item">
              <div class="form-check">
                <input class="form-check-input" name="options" type="radio" :id="'option'+ option.id">
                <label class="form-check-label" :for="'option'+ option.id">{{ option.body }}</label>
              </div>
            </li>
          </ul>
        </div>
        <div class="row">
          <button @click="addQuestion" class="btn btn-primary">Add</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    input: Object
  },
  data: function () {
    return {
      question: this.input
    }
  },
  methods: {
    addQuestion () {
      console.log('add to server')
    }
  }
}
</script>
