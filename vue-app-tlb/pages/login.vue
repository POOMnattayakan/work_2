<template>
  <div><h1>Page Login</h1>
    <v-form v-model="valid">
      <v-text-field
        v-model="name"
        :rules="nameRules"
        :counter="10"
        label="Name"
        required
      />
      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="E-mail"
        required
      />
    </v-form>
    <v-btn color="teal lighten-3">Save</v-btn>
  </div>
</template>
<script>
export default {
  data() {
    return {
      id: 1,
      valid: false,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid',
      ],
    }
  },
}
</script>