<template>
  <form @submit.prevent="onSubmit">
    <input
      class="input"
      :class="{ ok: ok, error: error }"
      :type="typeInput"
      v-model.trim="value"
      @input="inpuValidatetHandler"
    />
    <button>Test</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      value: "",
      ok: false,
      error: false,
    };
  },
  props: {
    typeInput: {
      type: String,
      default: "text",
      validator(type) {
        return ["text", "tel", "email", "url"].indexOf(type) !== -1;
      },
    },
  },

  methods: {
    onSubmit() {
      console.log(this.value);
      console.log(this.typeInput);
    },

    isWhitespace(str) {
      return /^\s*$/.test(str);
    },

    inpuValidatetHandler() {
      switch (this.typeInput) {
        case "text": {
          console.log(this.typeInput);
          this.validateText();
          break;
        }
      }
    },

    validateText() {
      if (!this.isWhitespace(this.value)) {
        this.ok = true;
        this.error = false;
      } else {
        this.ok = false;
        this.error = true;
      }
    },
  },
};
</script>


<style>

.input:focus {
  outline: none;
}

.ok {
  border: 1px solid rgb(1, 214, 1);
  background-color:rgb(212, 255, 212) ;
}
.error {
  border: 1px solid red;
  background-color:rgb(255, 220, 220);
}
</style>