<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title text-center">KRS</h5>
            <form @submit.prevent="loginUser">
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Email</label>
                <input type="email" class="form-control" id="exampleInputEmail1" v-model="email" aria-describedby="emailHelp" required>
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" class="form-control" id="exampleInputPassword1" v-model="password" required>
              </div>
              <button type="submit" class="btn btn-primary">Login</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'; 

export default {
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    loginUser() {
      const userData = {
        email: this.email,
        password: this.password
      };

      axios.post('https://api-group7-prognet.manpits.xyz/api/login', userData)
      .then(response => {
        localStorage.setItem('user', response.data.token);
        this.redirectUser();
        alert('Login successful!');
      })
      .catch(error => {
        console.error('Login failed:', error);
        alert('Login failed. Please try again.');
      });
  },
  redirectUser() {
    const isUserLoggedIn = localStorage.getItem('user');

    if (isUserLoggedIn) {
      this.$router.push('/dashboard');
    }
  }
},
created() {
  this.redirectUser();
}
};
</script>

