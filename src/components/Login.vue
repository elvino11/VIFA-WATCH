<template>

<!--  <header>
    <RouterLink to="/home">
      <img
        alt="Vue logo"
        class="logo"
        src="@/assets/logo.png"
        width="200"
        height="200"
      />
    </RouterLink>


    <div class="wrapper">
      <nav>
        <RouterLink to="/">Login</RouterLink>
        <RouterLink to="/register">Register</RouterLink>
        <RouterLink to="/home">Home</RouterLink>
        <RouterLink to="/product">Product</RouterLink>
        <RouterLink to="/brand">Brand</RouterLink>
        <RouterLink to="/testing">Adding</RouterLink>
        <RouterLink to="/cart">Transaction</RouterLink>
        <RouterLink to="/transaction">History Transaction</RouterLink>
        <RouterLink to="/about">About</RouterLink>


      </nav>

    </div>
  </header>-->

  <section class="login">
    <div class="container-mt-6">
      <div class="row d-flex justify-content-center">
        <div class="col-md-4">
          <h2 style="color: #e54499; font-weight: bold">Login</h2>
          <p><IconWarning/> Gunakan Tema Hitam Untuk Tampilan Lebih Menarik</p>
          <div class="card px-5 py-5" style="border-radius: 30px; border-color:#e54499; border-width: 3px">
            <form>
              <div class="mb-3">
                <label for="exampleInputUsername" class="form-label">Username</label>
                <input type="text" class="form-control" id="exampleInputUsername" aria-describedby="emailHelp" placeholder="Username" v-model="username">
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password" v-model="password">
              </div>
              <p style="color: black">Don't have an account ? <RouterLink to="/register">Register</RouterLink></p>
<!--              <RouterLink :to="{name: 'home', params: {status: this.status}}">-->
                <button type="button" class="btn-login" @click="login">LOGIN</button>
<!--              </RouterLink>-->

              <div class="succes-login" v-if="status" align="center">
                <RouterLink :to="{name: 'home', params: {status: this.status, id_user: this.id_user}}">
                  <a><h5><IconCheck/>Login Succes</h5></a>
                </RouterLink>
              </div>
            </form>
          </div>
        </div>

      </div>

    </div>

  </section>




<!--  <div class="username-input">
    <div class="mb-3">
      <label for="username" class="form-label">Username</label>
      <input type="text" class="form-control" id="username" placeholder="Username" v-model="this.username">
      <button type="button" class="btn btn-success" @click="search">Success</button>
    </div>
  </div>-->

<!--  <section class="user-info">
    <div v-if="user">
      <div class="content">
        <dl>
          <dt>Username</dt>
          <dd><strong>{{ user.username }}</strong></dd>

          <dt>No Handphone</dt>
          <dd><strong>{{ user.no_hp }}</strong></dd>

          <dt>Email</dt>
          <dd><strong>{{ user.email }}</strong></dd>

          <dt>Alamat</dt>
          <dd><strong>{{ user.alamat }}</strong></dd>

          <dt>Tanggal Lahir</dt>
          <dd><strong>{{ user.tanggal_lahir }}</strong></dd>

          <dt>Jenis Kelamin</dt>
          <dd><strong>{{ user.jenis_kelamin }}</strong></dd>

          <dt>Created At</dt>
          <dd><strong>{{ user.created_at }}</strong></dd>
        </dl>
        <hr>
      </div>
    </div>

    <div v-else>
      <div class="false">
        Maaf user dengan username : {{this.username}} tidak tersedia
      </div>
    </div>

    <div v-if="isLoading">
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
  </section>-->



</template>

<script>
import IconWarning from "./icons/IconWarning.vue";
import IconCheck from "./icons/IconCheck.vue";
export default {
  name: "Login",
  components: { IconCheck, IconWarning },
  data() {
    return{
      user : null,
      id_user: 0,
      status: false,
      username : null,
      password: null,
      isLoading: false
    }
  },
  methods: {
    login() {
      this.load();
    },
    load() {
      this.isLoading = true;
      fetch(`https://vifawatch.000webhostapp.com/pages/users/login.php?username=${this.username}&password=${  this.password}`, {
        method: 'GET',
      })
      .then(response => {
        if (response.ok) {
          return response.json();
        }
      })
      .then(json => {
        /*this.user = json.data;*/
        this.status = json.status
        this.id_user = json.data.id_user
        /*console.log(this.user);*/
        console.log(this.status);
        console.log(this.id_user);
      })
      .catch(()=> {
        alert('Login Failed')
      })
      .finally(() => {
        this.isLoading = false;
      })
    }
  },
  /*mounted() {
    this.load();
  }*/
};
</script>

<style scoped>
.login{
  margin-top: 100px;
}

.form-label{
  font-weight: bold;
  color: #e54499;
}
.btn-login{
  background-color: #e54499;
  border-color: #e54499;
  color: white;
  font-weight: bold;
}

</style>
