<template>
  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="name"
      :counter="10"
      :rules="nameRules"
      label="First Name"
      required
    ></v-text-field>
    <v-text-field
      v-model="lastName"
      :counter="15"
      :rules="lNameRules"
      label="Last Name"
      maxlength="20" 
      required
    ></v-text-field>
    <v-text-field
      v-model="phoneNumber"
      :rules="phoneRules"
      label="Phone Number"
      maxlength="13" 
      required
    ></v-text-field>

    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="E-mail"
      required
    ></v-text-field>
    <v-text-field
      v-model="password"
      autocomplete="current-password"
      :value="userPassword"
      label="Enter password"
      hint="Your password passed! Password rules are not meant to be broken!"
      :type="show1 ? 'password' : 'text'"
      :rules="[rules.password]"
      :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
      @click:append="() => (show1 = !show1)"
    ></v-text-field>
    <v-text-field
      v-model="rePassword"
      autocomplete="current-password"
      :value="passwordConfirm"
      label="Re-Enter password"
      hint="Your password passed! Password rules are not meant to be broken!"
      :type="show2 ? 'password' : 'text'"
      :rules="pwdConfirm"
      :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
      @click:append="() => (show2 = !show2)"
    ></v-text-field>

    <v-select
      v-model="select"
      :items="items"
      :rules="[v => !!v || 'Item is required']"
      label="Item"
      required
    ></v-select>

    <v-checkbox
      v-model="checkbox"
      :rules="[v => !!v || 'You must agree to continue!']"
      label="Do you agree?"
      required
    ></v-checkbox>

    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="validate"
    >
      Validate
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="reset"
    >
      Reset Form
    </v-btn>

    <v-btn
      color="warning"
      @click="resetValidation"
    >
      Reset Validation
    </v-btn>
  </v-form>
</template>

<script>
export default {
	name : "Register",
	data() {
		return {
      valid: true,
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10 && v.length >= 4) || 'Name must be more than 4 and less than 10 characters',
      ],
      lNameRules: [
        v => !!v || 'Last Name is required',
        v => (v && v.length <= 15 && v.length >= 4) || 'Name must be more than 4 and less than 15 characters',
      ],
      phoneRules: [
        v => !!v || 'Phone number is required',
        v => /^(\+98|0098|98|0)?9\d{9}$/.test(v) || 'phone number must start with 09 , 9 , +989 '
      ],
      emailRules : [
        v => !!v || 'Email is required',
        v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
      ],
        items: [
          'Florida',
          'Georgia',
          'Nebraska',
          'California',
          'New York',
        ],
      userPassword: "",
      value: true,
      rules: {
        required: value => !!value || "Required.",
        password: value => {
          const pattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.{8,})/;
          return (
            pattern.test(value) ||
            "Min. 8 characters with at least one capital letter, a number ."
          );
        }
      },
      pwdConfirm:[ v => !!v || 'Confirm password', v => v === this.password || 'Passwords do not match'],
      show1: false,
      show2: false,
      checkbox: false
		}
	},
    methods: {
    validate () {
      this.$refs.form.validate()
    },
    reset () {
      this.$refs.form.reset()
    },
    resetValidation () {
      this.$refs.form.resetValidation()
    },
  },
}
</script>