<template>
  <v-container>
    <v-layout>
      <v-flex xs12>
        <h1>Register form</h1>
        <form>
          <v-text-field
            v-model="english"
            :error-messages="englishErrors"
            label="English"
            required
            outline
            @input="$v.english.$touch()"
            @blur="$v.english.$touch()"
            @keyup="wordsCounter"
          ></v-text-field>
          <p>current word counter: {{currentWordsCount}}</p>
          <v-text-field
            v-model="translation"
            :error-messages="translationErrors"
            label="Translation"
            required
            outline
            @input="$v.translation.$touch()"
            @blur="$v.translation.$touch()"
          ></v-text-field>
          <v-btn @click="submit">submit</v-btn>
          <v-btn @click="clear">clear</v-btn>
        </form>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, maxLength, email } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],

  validations: {
    name: { required, maxLength: maxLength(10) },
    email: { required, email },
    select: { required },
    english: { required },
    translation: { required },
    checkbox: {
      checked(val) {
        return val;
      }
    }
  },

  data: () => ({
    name: "",
    currentWordsCount: 0,
    email: "",
    english: "",
    translation: "",
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: false
  }),

  computed: {
    checkboxErrors() {
      const errors = [];
      if (!this.$v.checkbox.$dirty) return errors;
      !this.$v.checkbox.checked && errors.push("You must agree to continue!");
      return errors;
    },
    selectErrors() {
      const errors = [];
      if (!this.$v.select.$dirty) return errors;
      !this.$v.select.required && errors.push("Item is required");
      return errors;
    },
    englishErrors() {
      const errors = [];
      if (!this.$v.english.$dirty) return errors;
      !this.$v.english.required && errors.push("English is required");
      return errors;
    },
    translationErrors() {
      const errors = [];
      if (!this.$v.translation.$dirty) return errors;
      !this.$v.translation.required && errors.push("Translation is required");
      return errors;
    },
    nameErrors() {
      const errors = [];
      if (!this.$v.name.$dirty) return errors;
      !this.$v.name.maxLength &&
        errors.push("Name must be at most 10 characters long");
      !this.$v.name.required && errors.push("Name is required.");
      return errors;
    },
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Must be valid e-mail");
      !this.$v.email.required && errors.push("E-mail is required");
      return errors;
    }
  },

  methods: {
    wordsCounter() {
      var wordsNum = this.english.split(" ").length;
      this.currentWordsCount = wordsNum;
    },
    submit() {
      this.$v.$touch();
    },
    clear() {
      this.$v.$reset();
      this.name = "";
      this.email = "";
      this.english = "";
      this.translation = "";
      this.select = null;
      this.checkbox = false;
    }
  }
};
</script>