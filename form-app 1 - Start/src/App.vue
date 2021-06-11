<template>
  <v-app>
    <v-container>
      <v-form>
        <v-container>
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field v-model="email" label="E-mail"></v-text-field>
            </v-col>
          </v-row>
          <v-btn class="mr-4">submit</v-btn>
          <v-btn>clear</v-btn>
        </v-container>
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

  validations: {
    email: { required, email },
  },
};
</script>
