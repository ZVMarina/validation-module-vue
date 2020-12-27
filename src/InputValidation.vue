<template>
  <div class="input-container">
    <input
      class="input"
      :class="{ validate: validate, error: error }"
      :type="typeInput"
      v-model.trim="value"
      @input="inpuValidatetHandler"
    />
    <span class="input__error">
      {{ textError }}
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: "",
      validate: false,
      error: false,
      textError: "",
    };
  },
  props: {
    typeInput: {
      type: String,
      default: "email",
      validator(type) {
        return ["text", "tel", "email", "url"].indexOf(type) !== -1;
      },
    },
  },

  methods: {
    isWhitespace(str) {
      return /^\s*$/.test(str);
    },

    isValidateTel(tel) {
      return /^(\+7|8)\s?(9\d{2}|\(9\d{2}\))(\s|-)?\d{3}\s?-?\d{2}\s?-?\d{2}$/.test(
        tel
      );
    },

    isValidateEmail(email) {
      return /^\w+(-\w+)?@\w+(\.\w+)?(-\w+)?\.[a-z]{2,}$/.test(email);
    },

    inpuValidatetHandler() {
      switch (this.typeInput) {
        case "text":
          console.log(this.typeInput);
          this.validateText();
          break;
        case "tel":
          console.log(this.typeInput);
          this.validateTel();
          break;
        case "email":
          console.log(this.typeInput);
          this.validateEmail();
          break;
      }
    },

    validateText() {
      if (!this.isWhitespace(this.value)) {
        this.validate = true;
      } else {
        this.validate = false;
      }
    },

    validateTel() {
      if (this.isValidateTel(this.value)) {
        this.validate = true;
      } else {
        this.validate = false;
      }
    },

    validateEmail() {
      if (this.isValidateEmail(this.value)) {
        this.validate = true;
      } else {
        this.validate = false;
      }
    },
  },
};
</script>


<style>
.input-container {
  position: relative;
}

.input__error {
  position: absolute;
  transform: translateY(100%);
  font-size: 12px;
  bottom: -5px;
  left: 0;
  color: red;
}

.input:focus {
  outline: none;
}

.validate {
  border: 1px solid rgb(1, 214, 1);
  background-color: rgb(212, 255, 212);
}
.error {
  border: 1px solid red;
  background-color: rgb(255, 220, 220);
}
</style>