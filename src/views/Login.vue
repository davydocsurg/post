<template>
  <div class="login">
    <div class="container col-md-6">
      <div class="card cardy shadow-lg px-4 py-4">
        <b-form @submit.prevent="signInUser" v-if="show">
        <!-- email -->
          <div class="mt-3 text-center"><h3>Sign In</h3></div>
            <div class="card-body log">
              <b-form-group
                class="text-left"
                id="input-group-1"
                label="Email address:"
                label-for="input-1"
                description="Enter a valid email address."
              >
                <b-form-input
                  id="input-1"
                  v-model="user.email"
                  type="email"
                  class="shadow-sm"
                  required
                  placeholder="Enter email address"
                ></b-form-input>
              </b-form-group>

        <!-- password -->
              <b-form-group id="input-group-2" label="Password:"
                label-for="input-2"
                class="text-left"
                description="Enter correct password."
              >
                <b-form-input
                  id="input-2"
                  v-model="user.password"
                  type="password"
                  class="shadow-sm"
                  required
                  placeholder="Enter password"
                ></b-form-input>
              </b-form-group>
                <b-button type="submit" class="btn" variant="btn btsg btn-lg btn-block">Sign In</b-button>
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
  name: 'login',

  data () {
    return {
      user: {
        email: '',
        password: ''
      },
      show: true
    }
  },
  methods: {
    signInUser () {
      // axios post request to laravel server
      axios.post('http://127.0.0.1:8000/api/auth/login', {
        email: this.user.email,
        password: this.user.password
      })
      // returns success message if found
        .then(function (response) {
          console.log(response)
        })
        // returns error message if found
        .catch(function (error) {
          console.log(error)
        })

      // resets the form
      this.user.email = ''
      this.user.password = ''
    }
  }
}
</script>
