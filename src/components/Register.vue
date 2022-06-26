<template>

<!--  <div class="register">
    <div class="mb-3">
      <label for="username" class="form-label">Username</label>
      <input type="text" class="form-control" id="username" placeholder="Username" v-model="userAdd.username">
    </div>
    <div class="mb-3">
      <label for="password" class="form-label">Password</label>
      <input type="password" class="form-control" id="password" placeholder="Password" v-model="userAdd.password">
    </div>
    <div class="mb-3">
      <label for="no_hp" class="form-label">No Handphone</label>
      <input type="number" class="form-control" id="no_hp" placeholder="No Handphone" v-model="userAdd.no_hp">
    </div>
    <div class="mb-3">
      <label for="email" class="form-label">Email</label>
      <input type="email" class="form-control" id="email" placeholder="email@example.com" v-model="userAdd.email">
    </div>
    <div class="mb-3">
      <label for="alamat" class="form-label">Alamat</label>
      <input type="text" class="form-control" id="alamat" placeholder="Alamat" v-model="userAdd.alamat">
    </div>

    <div class="mb-3">
      <label for="tanggal_lahir" class="form-label">Tanggal Lahir</label>
      <input type="date" class="form-control" id="tanggal_lahir" placeholder="DD/MM/YYYY" v-model="userAdd.tanggal_lahir">
    </div>
    <p>Jenis Kelamin</p>
    <div class="form-check">
      <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1" value="laki-laki" v-model="userAdd.jenis_kelamin">
      <label class="form-check-label" for="flexRadioDefault1">
        Laki - Laki
      </label>
    </div><p> {{userAdd.username}}</p>
    <p> {{userAdd.password}}</p>
    <p> {{userAdd.no_hp}}</p>
    <p> {{userAdd.email}}</p>
    <p> {{userAdd.alamat}}</p>
    <p> {{userAdd.tanggal_lahir}}</p>
    <p> {{userAdd.jenis_kelamin}}</p>
    <div class="form-check">
      <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault2" value="perempuan" v-model="userAdd.jenis_kelamin">
      <label class="form-check-label" for="flexRadioDefault2">
        Perempuan
      </label>
    </div>
    <button type="submit" class="btn btn-primary" @click="addUser">Register</button>
    <RouterLink  :to="{ name: 'login', params: {username: 'elvino'}}">
      <button type="button" class="btn btn-success">Success</button>
    </RouterLink>
  </div>-->

  <div class="container-mt-5">
    <div class="row d-flex justify-content-center">
      <div class="col-md-6">
        <h2 style="color: #e54499; font-weight: bold">Register</h2>
        <div class="card px-5 py-5" style="border-radius: 30px; border-color:#e54499; border-width: 3px">
          <div class="register">
            <div class="mb-3">
              <label for="username" class="form-label">Username</label>
              <input type="text" class="form-control" id="username" placeholder="Username" v-model="userAdd.username">
            </div>
            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <input type="password" class="form-control" id="password" placeholder="Password" v-model="userAdd.password">
            </div>
            <div class="mb-3">
              <label for="no_hp" class="form-label">No Handphone</label>
              <input type="number" class="form-control" id="no_hp" placeholder="No Handphone" v-model="userAdd.no_hp">
            </div>
            <div class="mb-3">
              <label for="email" class="form-label">Email</label>
              <input type="email" class="form-control" id="email" placeholder="email@example.com" v-model="userAdd.email">
            </div>
            <div class="mb-3">
              <label for="alamat" class="form-label">Alamat</label>
              <input type="text" class="form-control" id="alamat" placeholder="Alamat" v-model="userAdd.alamat">
            </div>
<!--            <p> {{userAdd.username}}</p>
            <p> {{userAdd.password}}</p>
            <p> {{userAdd.no_hp}}</p>
            <p> {{userAdd.email}}</p>
            <p> {{userAdd.alamat}}</p>
            <p> {{userAdd.tanggal_lahir}}</p>
            <p> {{userAdd.jenis_kelamin}}</p>-->
            <div class="mb-3">
              <label for="tanggal_lahir" class="form-label">Tanggal Lahir</label>
              <input type="date" class="form-control" id="tanggal_lahir" placeholder="DD/MM/YYYY" v-model="userAdd.tanggal_lahir">
            </div>
            <p style="color: #e54499; font-weight: bold">Jenis Kelamin</p>
            <div class="form-check">
              <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1" value="laki-laki" v-model="userAdd.jenis_kelamin">
              <label class="form-check-label" for="flexRadioDefault1">
                Laki - Laki
              </label>
            </div>
            <div class="form-check">
              <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault2" value="perempuan" v-model="userAdd.jenis_kelamin">
              <label class="form-check-label" for="flexRadioDefault2">
                Perempuan
              </label>
            </div>
            <div class="btn-register">
              <RouterLink to="/">
                <button type="submit" class="btn" @click="addUser">Register</button>
                <p style="color: black; margin-top: 10px">Have an account ? <RouterLink to="/">Login</RouterLink></p>
              </RouterLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Register",
  data(){
    return{
      data: [],
      userAdd: {
        username: '',
        password: '',
        no_hp : 0,
        email: '',
        alamat: '',
        tanggal_lahir: new Date().toISOString().slice(0, 10),
        jenis_kelamin: ''
      }
    }
  },
  methods: {
    addUser() {
      if (confirm("Are sure want to register ? ")) {
        const formUser = new URLSearchParams( {
          username: this.userAdd.username,
          password: this.userAdd.password,
          no_hp: this.userAdd.no_hp,
          email: this.userAdd.email,
          alamat: this.userAdd.alamat,
          tanggal_lahir: this.userAdd.tanggal_lahir,
          jenis_kelamin: this.userAdd.jenis_kelamin
        });
        console.log(this.userAdd.username);
        fetch(`https://vifawatch.000webhostapp.com/pages/users/create.php`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: formUser.toString(),
        })
          .then(response => {
            return response.json();
          })
          .then(json => {
            if (!json.status) {
              alert(json.error);
            } else {
              this.data.push(json.data);
              console.log(this.data);
            }
          })
          .catch((e) => {
            alert('Terjadi Error'+e.toString())
          })
          .finally(() => {
            this.userAdd.username = '';
            this.userAdd.password = '';
            this.userAdd.no_hp = 0;
            this.userAdd.email = '';
            this.userAdd.alamat = '';
            this.userAdd.jenis_kelamin = '';
          })
      }
    }
  }
};
</script>

<style scoped>
.form-check{
  margin-bottom: 15px;
}
.btn-register{
  margin-top: 30px;
}
.btn{
  background-color: #e54499;
  color: white;
  font-weight: bold;
}
.form-label{
  font-weight: bold;
  color: #e54499;
}
.form-check-label{
  color: black;
}
.container-mt-5{
  padding-top: 50px;
}
</style>

