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
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="username"
                label="Username"
                @blur="$v.username.$touch()"
                :error-messages="usernameErrors"
              ></v-text-field>
            </v-col>
          </v-row>
          <v-btn class="mr-4" @click="submit">submit</v-btn>
          <v-btn @click="clear">clear</v-btn>
        </v-container>
      </v-form>
    </v-container>
  </v-app>
</template>

<script>
// IMPORT
import { required, email, minLength, alphaNum } from 'vuelidate/lib/validators';

export default {
  name: 'App',

  data: () => ({
    email: '',
    username: '',
  }),
  methods: {
    submit() {
      this.$v.$touch();
      if (!this.$v.$invalid) console.log('submitted');
    },

    clear() {
      this.email = '';
      this.username = '';
      this.$v.$reset()
    },
  },

  validations: {
    email: { required, email },
    username: { required, minLength: minLength(8), alphaNum },
  },

  computed: {
    emailErrors() {
      let errors = [];
      if (!this.$v.email.$dirty) return errors;
      if (!this.$v.email.email) errors.push('Your email is wrong!');
      if (!this.$v.email.required) errors.push('You need to provide an email!');
      return errors;
    },

    usernameErrors() {
      let errors = [];

      if (!this.$v.username.$dirty) return errors;
      if (!this.$v.username.alphaNum)
        errors.push(
          'Your username should consist only of letters and numbers!'
        );
      if (!this.$v.username.minLength)
        errors.push('Your username should have at least 8 character! ');
      if (!this.$v.username.required)
        errors.push('You need to provide a username!');
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
