<template>
    <div class="container">
        <div class="row TimaVelikolepniy">
            <div class="col-md-6 mt-5 mx-auto">
                <form v-on:submit.prevent="login">
                    <h1 class="h3 mb-3 font-weight-normal">Please sign in</h1>
                    <div class="form-group">
                        <label for="email">Email Address</label>
                        <input type="email" v-model="email" class="form-control" name="email" placeholder="Enter Email">
                    </div>
                    <div class="form-group">
                        <label for="password">Password</label>
                        <input type="password" v-model="password" class="form-control" name="password" placeholder="Enter Password">
                    </div>
                    <button class="btn btn-lg btn-primary btn-block">Sign in</button>
                </form>
            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios'
import EventBus from './EventBus'

export default {
  data () {
    return {
      email: '',
      password: ''
    }
  },

  methods: {
    login () {
      axios.post('http://127.0.0.1:5000/users/login', {
        email: this.email,
        password: this.password
      }).then(res => {
        localStorage.setItem('token', res.data.token)
        this.email = ''
        this.password = ''
        this.$router.push('/')
      }).catch(err => {
        console.log(err)
      })
      this.emitMethod()
    },
    emitMethod () {
      EventBus.$emit('logged-in', 'loggedin')
    }
  }
}

</script>

<style lang="scss" scoped>
  .TimaVelikolepniy{
    padding: 4em 0;
    .col{
      float: initial;
      margin: 0 auto 0;
    }
  }
</style>