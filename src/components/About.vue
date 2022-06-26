<template>

  <header v-if="status">
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
        <RouterLink :to="{name: 'home', params: {status: this.status, id_user: this.id_user}}">Home</RouterLink>
        <RouterLink :to="{name: 'adding', params: {status: this.status, id_user: this.id_user}}">Adding</RouterLink>
        <RouterLink :to="{name: 'cart', params: {status: this.status, id_user: this.id_user}}">Transaction</RouterLink>
        <RouterLink :to="{name: 'transaction', params: {status: this.status, id_user: this.id_user}}">History Transaction</RouterLink>
        <RouterLink :to="{name: 'about', params: {status: this.status, id_user: this.id_user}}">About</RouterLink>
      </nav>

    </div>
  </header>



  <section class="login" v-if="status">

    <section class="user-info">
      <div v-if="user" align="center">
        <div class="card" style="width: 600px; height: 600px">
          <div class="gambar" align="center">
            <img src="/src/assets/img_avatar.png" id="gambar" alt="Avatar" style="width: 200px; height: 200px;">
          </div>
          <div class="container">
            <h4><b>Username : {{ user.username }}</b></h4>
            <p>Tanggal Lahir : {{ user.tanggal_lahir }}</p>
            <p>Alamat : {{ user.alamat }}</p>
            <p>No Handphone : {{ user.no_hp }}</p>
            <p>emai : {{ user.email }}</p>
            <p>Jenis Kelamin : {{ user.jenis_kelamin }}</p>
            <p>Dibuat : {{ user.created_at }}</p>

          </div>
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
    </section>
  </section>

  <section v-else class="unLogin">
    <h1>
      Anda Harus Login Terlebih Dahulu
      <RouterLink to="/">Di Sini</RouterLink>
    </h1>
  </section>

</template>

<script>
export default {
  name: "About",
  data() {
    return {
      user: null,
      status : this.$route.params.status,
      id_user: this.$route.params.id_user,
      isLoading: false
    }
  },
  methods: {
    load() {
      this.isLoading = true;
      fetch(`http://localhost/fetano/pages/users/get.php?id_user=${this.id_user}`, {
        method: 'GET',
      })
        .then(response => {
          if (response.ok) {
            return response.json();
          }
        })
        .then(json => {
          /*this.user = json.data;*/
          this.user = json.data;
          /*console.log(this.user);*/
          console.log(this.user);
          console.log(this.status);
          console.log(this.id_user);
          const images = ["/src/assets/img_avatar.png", "/src/assets/img_avatar2.png"];
        /*  const cekJenis = json.data.jenis_kelamin;
          console.log(cekJenis);

          if (cekJenis === "laki-laki") {
            document.getElementById("gambar").src = images[0];
          } else {
            document.getElementById("gambar").src = images[1];
          }
*/
        })
        .catch(()=> {
          alert('Login Failed')
        })
        .finally(() => {
          this.isLoading = false;
        })
    }
  },
  mounted() {
    this.load();
  }
};
</script>

<style scoped>
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
.card {
  /* Add shadows to create the "card" effect */
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  color: black;
  border-color: #e54499;
  border-width: 3px;
}

/* On mouse-over, add a deeper shadow */
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

/* Add some padding inside the card container */
.container {
  padding: 2px 16px;
}
.gambar{
  margin-top: 30px;
  margin-bottom: 30px;
}
.user-info {
  margin-top: 50px;
  margin-bottom: 50px;
}
</style>
