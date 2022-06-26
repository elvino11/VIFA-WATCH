<template>

  <section class="login" v-if="status">
    <div class="back">
      <h5>
        <RouterLink :to="{name: 'home', params: {status: this.status, id_user: this.id_user}}">
          <IconBack/> Go back to home
        </RouterLink>

      </h5>
    </div>

    <section class="product" v-if="product">
      <div class="product-detail">
        <div align="center" class="product-img">
          <img :src="product.gambar" width="400" height="600">
        </div>
        <div class="detail">
          <h2>{{product.nama_barang}}</h2>
          <h3>Rp {{product.harga}}</h3>
          <h4>Stok : {{product.stok_barang}}</h4>
        </div>
      </div>
      <div class="deskripsi-product">
        <div class="deskripsi">
          <h4 style="color: var(--color-heading); text-decoration-line: underline">PRODUCT DESCRIPTION</h4>
          <h6 style="text-align: justify; padding-top: 5px">{{product.deskripsi}}</h6>
        </div>
        <div class="upddlt-product">
          <h4 style="color: var(--color-heading); text-decoration-line: underline">UPDATE & DELETE PRODUCT</h4>
          <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal" data-bs-whatever="@mdo" style="margin-right: 30px">Edit</button>
          <RouterLink :to="{name: 'home', params: {status: this.status, id_user: this.id_user}}">
            <button class="btn btn-danger" @click="remove">REMOVE</button>
          </RouterLink>
        </div>
      </div>
    </section>

    <section v-else>
      <div class="false">
        Maaf produk dengan kode barang : {{this.kode_barang}} tidak tersedia
      </div>
    </section>





    <!--  Update Produk-->


    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Update Product</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body" v-if="product">
            <form @submit.prevent="update">
              <div class="mb-3">
                <label for="nama_barang" class="col-form-label">Nama Barang</label>
                <input type="text" class="form-control" id="nama_barang" :placeholder="product.nama_barang" v-model="formEdit.nama_barang">
              </div>
              <p>Brand</p>
              <select class="form-select" aria-label="Default select example" v-model="formEdit.brand">
                <option selected disabled value="0">{{ product.brand.nama_brand }}</option>
                <option v-for="brand in brands" :value="brand.id">{{ brand.nama_brand }}</option>
              </select>
              <div class="mb-3">
                <label for="stok_barang" class="col-form-label">Stok Barang</label>
                <input type="number" class="form-control" id="stok_barang" :placeholder="product.stok_barang" v-model="formEdit.stok_barang">
              </div>
              <div class="mb-3">
                <label for="harga_barang" class="col-form-label">Harga Barang</label>
                <input type="number" class="form-control" id="harga_barang" :placeholder="product.harga" v-model="formEdit.harga">
              </div>
              <div class="mb-3">
                <label for="tanggal_lahir" class="form-label">Tanggal Lahir</label>
                <input type="date" class="form-control" id="tanggal_lahir" :placeholder="product.tanggal" v-model="formEdit.tanggal">
              </div>
              <div class="mb-3">
                <label for="deskripsi" class="col-form-label">Deskripsi</label>
                <textarea class="form-control" id="deskripsi" :placeholder="product.deskripsi" v-model="formEdit.deskripsi"></textarea>
              </div>
              <div class="mb-3">
                <label for="gambar" class="col-form-label">Link Gambar</label>
                <input type="text" class="form-control" id="gambar" :placeholder="product.gambar" v-model="formEdit.gambar">
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <!--          <RouterLink to="/home">
                        <button class="btn btn-success" @click="update">Update</button>
                      </RouterLink>-->
            <RouterLink :to="{name: 'home', params: {status: this.status, id_user: this.id_user}}">
              <button type="button" class="btn btn-primary" @click="update">Update</button>
            </RouterLink>
          </div>
        </div>
      </div>
    </div>

    <div v-if="isLoading">
      <div class="spinner-border text-primary" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>


    <div class="buy">
      <h4 style="color: var(--color-heading); text-decoration-line: underline; padding-bottom: 20px">ADD TO TRANSACTION</h4>
      <p><IconWarning/> Harap Masukkan ID Transaksi, jika mau beli jam dengan jenis berbeda masukkan ID Transaksi yang sama dalam 1 kali transaksi</p>
      <button class="btn btn-danger" @click="min">MIN</button>
      <input type="number" v-model="addChart.kuantitas">
      <button class="btn btn-success" @click="add">PLUS</button>
      <input type="text" v-model="addChart.id_transaksi" placeholder="ID Transaksi" style="margin-left: 30px">
      <RouterLink :to="{name: 'cart', params: {id_transaksi : addChart.id_transaksi, status: this.status, id_user: this.id_user}}">
        <button class="btn btn-success" @click="buyProduct">BUY</button>
      </RouterLink>
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
import IconWarning from "./icons/IconWarning.vue";
import IconBack from "./icons/IconBack.vue";
export default {
  name: "ProdukDetail",
  components: { IconBack, IconWarning },
  data() {
    return {
      brands: [],
      product: null,
      data: [],
      index: this.$route.params.index,
      status: this.$route.params.status,
      id_user: this.$route.params.id_user,
      selectedIndex: -1,
      kode_barang: this.$route.params.kode_barang,
      isLoading: false,
      formEdit: {
        kode_barang: this.$route.params.kode_barang,
        nama_barang: '',
        brand: 0,
        stok_barang: '',
        harga: '',
        tanggal: new Date().toISOString().slice(0, 10),
        deskripsi: '',
        gambar: ''
      },
      addChart: {
        id_transaksi: '',
        id_user: this.$route.params.id_user,
        kode_barang: this.$route.params.kode_barang,
        kuantitas: 1
      }
    }
  },
  methods: {
    add() {
      this.addChart.kuantitas++;
    },
    min() {
      if (this.addChart.kuantitas > 0) {
        this.addChart.kuantitas;
      } else {
        this.addChart.kuantitas = 0;
      }
    },
    buyProduct() {
      if (confirm("are you sure want to add to cart ?")) {
        const formChart = new URLSearchParams( {
          id_user: this.addChart.id_user,
          kode_barang: this.addChart.kode_barang,
          kuantitas: this.addChart.kuantitas,
          id_transaksi : this.addChart.id_transaksi
        });
        fetch(`http://localhost/fetano/pages/keranjang/create.php`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: formChart.toString(),
        })
        .then(response => {
          return response.json();
        })
        .then(json => {
          if (!json.status) {
            alert(json.error)
          } else {
            this.data.push(json.data);
            console.log(this.data);
          }
        })
        .catch((e) => {
          alert("Terjadi Error" + e.toString())
        })
        .finally(() => {
          this.addChart.kuantitas = 1;
          this.addChart.id_transaksi = '';
        })
      }
    },
    ProductDetail() {
      this.isLoading = true;
      fetch(`https://vifawatch.000webhostapp.com/pages/products/get.php?kode_barang=${this.kode_barang}`, {
        method: 'GET',
      })
        .then(response => {
          if (response.ok) {
            return response.json();
          }
        })
        .then(json => {
          this.product = json.data;
          console.log(this.product);
        })
        .catch(() => {
          alert('Terjadi Error')
        })
        .finally(() => {
          this.isLoading = false;
        })
    },
    loadProduct() {
      this.isLoading = true;
      fetch(`https://vifawatch.000webhostapp.com/pages/brands/index.php`, {
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
    remove() {
      if (confirm("are you sure want to delete ?")) {
        const removeProduct = new URLSearchParams({
          'kode_barang': this.kode_barang
        });
        fetch(`https://vifawatch.000webhostapp.com/pages/products/delete.php`, {
          method: 'DELETE',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: removeProduct.toString(),
        })
          .then(response => {
            if (response.ok) {
              this.data.splice(this.index, 1);
            }
            return response.json();
          })
          .then(json => {
            if (!json.status) {
              alert(json.error);
            }
          })
          .catch(() => {
            alert('Terjadi Error')
          })
      }
    },
    update() {
      if (confirm("are you sure want to update?")) {
        const updateProduct = new URLSearchParams({
          kode_barang: this.formEdit.kode_barang,
          nama_barang: this.formEdit.nama_barang,
          brand: this.formEdit.brand,
          stok_barang: this.formEdit.stok_barang,
          harga: this.formEdit.harga,
          tanggal: this.formEdit.tanggal,
          deskripsi: this.formEdit.deskripsi,
          gambar: this.formEdit.gambar
        });
        fetch(`https://vifawatch.000webhostapp.com/pages/products/update.php`, {
          method: 'PATCH',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: updateProduct.toString(),
        })
        .then(response => {
          return response.json()
        })
        .then(json => {
          if (!json.status) {
            alert(json.error);
          } else {
            /*
            Update data
             */
            this.data[this.index] = json.data;
            console.log(this.kode_barang);
          }
        })
        .catch((e) => {
          alert('Terjadi error' + e.toString())
        })
        .finally(() => {
        })
      }
    }
  },
  mounted() {
    this.ProductDetail();
    this.loadProduct();
  }
};
</script>

<style scoped>
.modal-dialog{
  color: black;
}
.product-detail{
  background-image: url("https://content.rolex.com/dam/2021/bg/model-cover-background-variations-steel.jpg?imwidth=1920");
  border-radius: 10px;
}
.detail{
  color: white;
  margin-left: 60px;
  padding-bottom: 30px;
}
.deskripsi-product{
  padding-top: 50px;
  display: flex;
  /*width: 50%;*/
  padding-bottom: 50px;
}
.deskripsi{
  width: 50%;
  margin-right: 30px;
}
.buy{
  padding-bottom: 50px;
}
.product{
  margin-top: 50px;
}
.back{
  padding-top: 50px;
}
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
</style>
