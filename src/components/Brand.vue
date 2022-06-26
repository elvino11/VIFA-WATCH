<template>


  <section class="login" v-if="status">
    <div class="title" style="margin-bottom: 30px; margin-top: 30px">
      <h1 style="color: #e54499">AVAILABLE BRAND</h1>
      <hr/>
    </div>


    <div style="display: flex">
      <div v-for="(brand, index) in brands">
        <!--    {{brand.nama_brand}}
            {{index}}
            {{brand.id}}
            <img :src="brand.gambar_brand" width="100" height="100">-->
        <div class="brand">
          <div class="card" style="width: 150px; height: 270px; border-color: #e54499; border-width: 2px">
            <img :src="brand.gambar_brand" class="card-img-top" alt="..." width="100" height="100">
            <div class="card-body">
              <h5 align="center" class="card-title" style="color: black">{{ brand.nama_brand }}</h5>
            </div>
            <button type="button" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#exampleModal" data-bs-whatever="@mdo" @click="showUpdate(brand.id)">Edit</button>
            <button type="button" class="btn btn-danger" data-bs-toggle="modal" data-bs-target="#exampleModal1" @click="showDelete(brand.id)">DELETE</button>
          </div>
        </div>
      </div>
    </div>



    <!--  Update Produk-->
    <div>
      <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">Update Product</h5>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
              <form @submit.prevent="updateBrand(index)">
                <div class="mb-3">
                  <label for="nama_brandUPD" class="col-form-label">Nama Brand</label>
                  <input type="text" class="form-control" id="nama_brandUPD"  v-model="brandUpdate.nama_brand">
                </div>
                <div class="mb-3">
                  <label for="gambar_brandUPD" class="col-form-label">Gambar Brand</label>
                  <input type="text" class="form-control" id="gambar_brandUPD" v-model="brandUpdate.gambar_brand">
                </div>
              </form>
              <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                <!--          <RouterLink to="/home">
                            <button class="btn btn-success" @click="update">Update</button>
                          </RouterLink>-->
                <button type="button" class="btn btn-primary" @click="updateBrand(index)">Update</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>




    <div v-for="(brand, index) in brands">
      <!-- Button trigger modal -->


      <!-- Modal -->
      <div class="modal fade" id="exampleModal1" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel1">Modal title</h5>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
              Are you sure want to delete ?
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
              <button type="button" class="btn btn-primary" @click="removeBrand(index)">Delete</button>
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








<!--  <div>
    <button @click="showAddBrand">Add</button>
  </div>
&lt;!&ndash;  <div v-if="model">&ndash;&gt;
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
                  <button type="submit" class="btn btn-primary" @click="addBrand">Add</button>
                </RouterLink>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>-->
<!--  </div>-->


</template>

<script>
export default {
  name: "Brand",
  data() {
    return {
      brands: [],
      data: [],
      model: false,
      isLoading: false,
      id_user: this.$route.params.id_user,
      status: this.$route.params.status,
      brandAdd: {
        nama_brand: '',
        gambar_brand: ''
      },
      brandUpdate: {
        id: 0,
        nama_brand: '',
        gambar_brand: ''
      },
      brandDelete: {
        id: 0
      }
    }
  },
  methods: {
    showAddBrand() {
      this.model = true;
    },
    showUpdate(id) {
      return this.brandUpdate.id = id
    },
    showDelete(id) {
      return this.brandDelete.id = id
    },
    load() {
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
        console.log(this.brands[0].nama_brand);
      })
      .catch(() => {
        alert("Terjadi Error")
      })
      .finally(() => {
        this.isLoading = false;
      })
    },
    addBrand() {
      if (confirm("are you sure want to add brand ?")) {
        const formBrand = new URLSearchParams( {
          nama_brand: this.brandAdd.nama_brand,
          gambar_brand: this.brandAdd.gambar_brand
        })
        fetch(`https://vifawatch.000webhostapp.com/pages/brands/create.php`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: formBrand.toString(),
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
          alert('Terjadi error ' + e.toString() )
        })
        .finally(() => {
          this.brandAdd.nama_brand = '';
          this.brandAdd.gambar_brand = '';
          this.model = false;
        })
      }
    },
    updateBrand(index) {
      if (confirm("are you sure want to update ? ")) {
        const brandUpdate = new URLSearchParams( {
          id: this.brandUpdate.id,
          nama_brand: this.brandUpdate.nama_brand,
          gambar_brand: this.brandUpdate.gambar_brand
        });
        fetch(`https://vifawatch.000webhostapp.com/pages/brands/update.php`, {
          method: 'PATCH',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: brandUpdate.toString(),
        })
        .then(response => {
          return response.json();
        })
        .then(json => {
          if (!json.status) {
            alert(json.error);
          } else {
            /*
            Update Data
             */
            this.data[index] = json.data;
            console.log(brandUpdate.id);
          }
        })
        .catch((e) => {
          alert("Terjadi Error " + e.toString())
        })
        .finally(() => {
          alert("Data Berhasil Diupdate")
        })
      }
    },
    removeBrand(index) {
      if (confirm("are you sure want to delete ? ")) {

        const brandRemove = new URLSearchParams( {
          id : this.brandDelete.id
        });
        fetch(`https://vifawatch.000webhostapp.com/pages/brands/delete.php`, {
          method: 'DELETE',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
            'API-Key': 'secret'
          },
          body: brandRemove.toString(),
        })
        .then(response => {
          if (response.ok) {
            this.data.splice(index, 1);
          }
          return response.json();
        })
        .then(json => {
          if (!json.status) {
            alert(json.error)
          }
        })
        .catch(() => {
          alert("Terjadi Error")
        })
      }
    },
  },
  mounted() {
    this.load();
  }
};
</script>

<style scoped>
h1{
  color: var(--color-heading);
}
.btn-addBrand{
  margin-top: 30px;
}
.form-label{
  font-weight: bold;
  color: #e54499;
}
.modal-dialog{
  color: black;
}
.brand{
  margin-right: 30px;
}
.unLogin {
  margin-top: 100px;
  color: var(--color-heading);
}
</style>
