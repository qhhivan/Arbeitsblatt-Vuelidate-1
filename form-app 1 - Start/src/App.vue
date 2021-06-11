<template>
  <v-app>
    <v-container>
      <v-form>
        <v-container>
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="email"
                label="E-mail"
                @input="$v.email.$touch()"
                @blur="$v.email.$touch()"
                :error-messages="emailErrors"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-btn class="mr-4" @click="submit">submit</v-btn>
          <v-btn @click="clear">clear</v-btn>
        </v-container>
        <!-- <p v-if="$v.email.required == false">Bitte Email-Adresse angeben</p>
        <p v-if="$v.email.required == true && $v.email.email == false">
          Bitte Email-Adresse richtig Ausfühlen
        </p> -->
      </v-form>
    </v-container>
  </v-app>
</template>

<script>
// IMPORT
import { required, email } from 'vuelidate/lib/validators';

export default {
  name: 'App',

  data: () => ({
    email: '',
  }),
  methods: {
    submit() {
      this.$v.$touch();
      if (!this.$v.$invalid) console.log('submitted');
    },

    clear() {
      this.email = '';
    },
  },

  validations: {
    email: { required, email },
  },

  computed: {
    emailErrors() {
      let errors = [];
      if (!this.$v.email.$dirty) return errors;
      if (!this.$v.email.email) errors.push('Your email is wrong!');
      if (!this.$v.email.required) errors.push('You need to provide an email!');
      return errors;
    },
  },
};
</script>
<style>
p {
  color: red;
}
</style>
