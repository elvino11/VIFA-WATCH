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


  <section class="sucLogin" v-if="status">

<!--    <RouterLink :to="{name: 'home', params: {bisa: this.bisa}}">Home</RouterLink>-->
    <div class="product">
      <div class="container-mt-5">
        <div class="row d-flex justify-content-center">
          <div class="col-md-6">
            <h2 style="color: #e54499; font-weight: bold">Add New Product</h2>
            <div class="card px-5 py-5" style="border-radius: 30px; border-color:#e54499; border-width: 3px">
              <div class="register">
                <div class="mb-3">
                  <label for="username" class="form-label">Kode Barang</label>
                  <input type="text" class="form-control" id="username" placeholder="Username" v-model="productAdd.kode_barang">
                </div>
                <div class="mb-3">
                  <label for="password" class="form-label">Nama Barang</label>
                  <input type="text" class="form-control" id="password" placeholder="Password" v-model="productAdd.nama_barang">
                </div>
                <p>Brand</p>
                <select class="form-select" aria-label="Default select example" v-model="productAdd.brand">
                  <option selected disabled value="0">Brand</option>
                  <option v-for="brand in brands" :value="brand.id">{{ brand.nama_brand }}</option>
                </select>
                <div class="mb-3">
                  <label for="email" class="form-label">Stok Barang</label>
                  <input type="number" class="form-control" id="email" placeholder="email@example.com" v-model="productAdd.stok_barang">
                </div>
                <div class="mb-3">
                  <label for="alamat" class="form-label">Harga</label>
                  <input type="number" class="form-control" id="alamat" placeholder="Alamat" v-model="productAdd.harga">
                </div>
                <div class="mb-3">
                  <label for="tanggal_lahir" class="form-label">Tanggal</label>
                  <input type="date" class="form-control" id="tanggal_lahir" placeholder="DD/MM/YYYY" v-model="productAdd.tanggal">
                </div>
                <div class="mb-3">
                  <label for="deskripsi" class="form-label">Deskripsi</label>
                  <textarea type="text" class="form-control" id="deskripsi" placeholder="DD/MM/YYYY" v-model="productAdd.deskripsi"></textarea>
                </div>
                <div class="mb-3">
                  <label for="gambar" class="form-label">Link Gambar</label>
                  <input type="text" class="form-control" id="gambar" placeholder="DD/MM/YYYY" v-model="productAdd.gambar">
                </div>
                <RouterLink to="/product">
                  <button type="submit" class="btn btn-success" @click="addProduct">Add</button>
                </RouterLink>
              </div>
            </div>
          </div>
        </div>
      </div>
<!--      <div class="mb-3">
        <label for="username" class="form-label">Kode Barang</label>
        <input type="text" class="form-control" id="username" placeholder="Username" v-model="productAdd.kode_barang">
      </div>
      <div class="mb-3">
        <label for="password" class="form-label">Nama Barang</label>
        <input type="text" class="form-control" id="password" placeholder="Password" v-model="productAdd.nama_barang">
      </div>
      <p>Brand</p>
      <select class="form-select" aria-label="Default select example" v-model="productAdd.brand">
        <option selected disabled value="0">Brand</option>
        <option v-for="brand in brands" :value="brand.id">{{ brand.nama_brand }}</option>
      </select>
      <div class="mb-3">
        <label for="email" class="form-label">Stok Barang</label>
        <input type="number" class="form-control" id="email" placeholder="email@example.com" v-model="productAdd.stok_barang">
      </div>
      <div class="mb-3">
        <label for="alamat" class="form-label">Harga</label>
        <input type="number" class="form-control" id="alamat" placeholder="Alamat" v-model="productAdd.harga">
      </div>
      <p> {{productAdd.username}}</p>
      <p> {{ productAdd.nama_barang }}</p>
      <p> {{ productAdd.brand }}</p>
      <p> {{ productAdd.stok_barang }}</p>
      <p> {{ productAdd.harga }}</p>
      <p> {{ productAdd.tanggal }}</p>
      <p> {{ productAdd.deskripsi }}</p>
      <p> {{productAdd.gambar}}</p>
      <div class="mb-3">
        <label for="tanggal_lahir" class="form-label">Tanggal</label>
        <input type="date" class="form-control" id="tanggal_lahir" placeholder="DD/MM/YYYY" v-model="productAdd.tanggal">
      </div>
      <div class="mb-3">
        <label for="deskripsi" class="form-label">Deskripsi</label>
        <textarea type="text" class="form-control" id="deskripsi" placeholder="DD/MM/YYYY" v-model="productAdd.deskripsi"></textarea>
      </div>
      <div class="mb-3">
        <label for="gambar" class="form-label">Link Gambar</label>
        <input type="text" class="form-control" id="gambar" placeholder="DD/MM/YYYY" v-model="productAdd.gambar">
      </div>-->

      <!--      <div class="input-group mb-3">
              <label class="input-group-text" for="gambar">Gambar</label>
              <input type="file" class="form-control" id="gambar">
            </div>-->

    </div>

<!--    <div>
      <button class="btn-success" @click="move">Home<RouterLink to="/" v-if="pindah">Pindah</RouterLink></button>
    </div>-->
    <div class="add-brand">
      <div class="container-mt-5">
        <div class="row d-flex justify-content-center">
          <div class="col-md-6">
            <h2 style="color: #e54499; font-weight: bold">Add New Brand</h2>
            <div class="card px-5 py-5" style="border-radius: 30px; border-color:#e54499; border-width: 3px">
              <div class="register">
                <div class="mb-3">
                  <label for="nama_brand" class="form-label">Nama Brand</label>
                  <input type="text" class="form-control" id="nama_brand" placeholder="Nama Brand" v-model="brandAdd.nama_brand">
                </div>
                <div class="mb-3">
                  <label for="gambar_brand" class="form-label">Link Gambar</label>
                  <input type="text" class="form-control" id="gambar_brand" placeholder="Link Gambar" v-model="brandAdd.gambar_brand">
                </div>
                <div class="btn-addBrand">
                  <RouterLink to="/home">
                    <button type="submit" class="btn btn-success" @click="addBrand">Add</button>
                  </RouterLink>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
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
  name: "Adding",
  data(){
    return{
      status: this.$route.params.status,
      id_user: this.$route.params.id_user,
      pindah: false,
      brands: [],
      data: [],
      productAdd: {
        kode_barang: '',
        nama_barang: '',
        brand : 0,
        stok_barang: 0,
        harga: 0,
        tanggal: new Date().toISOString().slice(0, 10),
        deskripsi: '',
        gambar: ''
      },
      brandAdd: {
        nama_brand: '',
        gambar_brand: ''
      },
    }
  },
  methods: {
    move() {
      this.pindah = true
    },
    addProduct() {
      if (confirm("Are you sure want to add ?")) {
        const formProduct = new URLSearchParams({
          kode_barang: this.productAdd.kode_barang,
          nama_barang: this.productAdd.nama_barang,
          brand: this.productAdd.brand,
          stok_barang: this.productAdd.stok_barang,
          harga: this.productAdd.harga,
          tanggal: this.productAdd.tanggal,
          deskripsi: this.productAdd.deskripsi,
          gambar: this.productAdd.gambar
          /*gambar: this.productAdd.gambar = $refs.gambar.files[0]*/

        });

        fetch(`http://localhost/fetano/pages/products/create.php`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: formProduct.toString(),
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
            this.productAdd.kode_barang = '';
            this.productAdd.nama_barang = '';
            this.productAdd.brand = 0;
            this.productAdd.stok_barang = 0;
            this.productAdd.harga = 0;
            this.productAdd.deskripsi = '';
            this.productAdd.gambar = ''
          })
      }
    },
    loadProduct() {
      this.isLoading = true;
      fetch(`http://localhost/fetano/pages/brands/index.php`, {
        method: 'GET',
      })
        .then(response => {
          if (response.ok) {
            return response.json();
          }
        })
        .then(json => {
          this.brands = json.data;
        })
        .catch(() => {
          alert("Terjadi Error")
        })
        .finally(() => {
          this.isLoading = false;
        })
    },
  },
  mounted() {
    this.loadProduct();
  }
};
</script>

<style scoped>
.add-brand{
  color: black;
  padding-bottom: 50px;
}
.product{
  color: black;
  padding-top: 50px;
  padding-bottom: 50px;
}
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
</style>
