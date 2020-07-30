<template>
  <div class="register">
    <div class="container col-md-6">
    <div variant="success" v-if="status === 201">User registered successfully</div>
    <div variant="danger" v-if="status === 400">Registration was unsuccessful</div>
       <!-- <form @submit.prevent="submit" v-if="!savingSuccessful"> -->
      <div class="card shadow-lg px-4">
        <b-form @submit.prevent="addUser"  v-if="show">
        <!-- name -->
        <div class="mt-3 text-center"><h3>Sign Up</h3></div>
          <div class="card-body log">
            <b-form-group id="input-group-1" label="Name:"
              label-for="input-2"
              class="text-left"
            >
              <b-form-input
                id="input-1"
                class="shadow-sm"
                v-model="user.name"
                required
                placeholder="Enter name"
              ></b-form-input>
            </b-form-group>

            <!-- email -->
            <b-form-group
              id="input-group-2"
              label="Email address:"
              label-for="input-2"
              class="text-left"
              description="We'll never share your email with anyone else."
            >
              <b-form-input
                id="input-2"
                v-model="user.email"
                type="email"
                class="shadow-sm"
                required
                placeholder="Enter email address"
              ></b-form-input>
            </b-form-group>

          <!-- password -->
            <b-form-group id="input-group-3" label="Password:"
              label-for="input-3"
              class="text-left"
              description="Password must be minimum of 8 characters."
            >
              <b-form-input
                id="input-3"
                v-model="user.password"
                type="password"
                class="shadow-sm"
                required
                placeholder="Enter password"
              ></b-form-input>
            </b-form-group>

          <!-- confirm_password -->
            <b-form-group id="input-group-4" label="Confirm Password:"
              label-for="input-4"
              class="text-left"
              description="Confirm password."
            >
              <b-form-input
                id="input-4"
                v-model="user.confirm_password"
                type="password"
                class="shadow-sm"
                required
                placeholder="Confirm password"
              ></b-form-input>
            </b-form-group>

          <b-button type="submit" variant=" btsg btn-block btn-lg">Sign Up</b-button>
          </div>
      </b-form>
    </div>
  </div>
</div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'

export default {
  name: 'register',

  data () {
    return {
      user: {
        name: '',
        email: '',
        password: '',
        confirm_password: ''
      },
      show: true,

      data: {
        status: [],
        message: ''
      }
    }
  },
  methods: {
    addUser () {
      this.data.status = []
      this.data.message = ''
      // axios post request
      axios.post('http://127.0.0.1:8000/api/auth/register', {
        name: this.user.name,
        email: this.user.email,
        password: this.user.password,
        password_confirmation: this.user.confirm_password
      })

      // promises
        .then(function (response) {
          console.log(response)
          if (response.status === 201) {
            this.data.message.push('User registered successfully')
          }
          // else {
          //   this.push('Something went wrong, please refresh and try again.')
          // }
        })
        .catch(function (error) {
          console.log(error)

          if (error.response.status === 400) {
            this.data.message.push('Registration failed')
          }
          // else {
          //   this.errors.push('Something went wrong, please refresh and try again.')
          // }
        })
      // resets the form
      this.user.name = ''
      this.user.email = ''
      this.user.password = ''
      this.user.confirm_password = ''
    }
  }
}
</script>
