<template>
  <div>
    <div class="clearfix">
      <div class="float-end">
        <button type="button" class="btn btn-secondary btn-lg">
          เพิ่มรายการสินค้า
        </button>
      </div>
    </div>
    <div class="container">
      <!-- banner -->
      <!-- Section-->

      <div>
        <h1 class="text-center mt-5">สินค้าของฉัน</h1>
        <div
          class="row gx-6 gx-lg-6 row-cols-6 row-cols-md-6 row-cols-xl-6 justify-content-center mt-5"
        >
          <div
            v-for="(item, i) in recommends"
            :key="i"
            class="card mx-auto col-md-3 col-10"
          >
            <img
              class="mx-auto img-thumbnail product-img"
              :src="item.image_url"
            />
            <div class="card-body text-center mx-auto">
              <h5 class="card-title">{{ item.title }}</h5>
              <p class="card-text">{{ item.price }}</p>
            </div>

            <button
              @click="showAlert"
              type="button"
              class="btn btn-outline-warning"
            >
              แก้ไข
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapActions, mapGetters } from "vuex";
export default {
  // data: () => ({
  //   item: [
  //     {
  //       image_url:
  //         "https://images.unsplash.com/photo-1520412099551-62b6bafeb5bb?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80",
  //       title: "ต้นไม้",
  //       price: "432",
  //     },
  //     {
  //       image_url:
  //         "https://images.unsplash.com/photo-1491147334573-44cbb4602074?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80",
  //       title: "ใบหญ้า",
  //       price: "243",
  //     },
  //     {
  //       image_url:
  //         "https://images.unsplash.com/photo-1506634064465-7dab4de896ed?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80",
  //       title: "ใบเหลียง",
  //       price: "143",
  //     },
  //     {
  //       image_url:
  //         "https://images.unsplash.com/photo-1453904300235-0f2f60b15b5d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=772&q=80",
  //       title: "ใบไม้",
  //       price: "523",
  //     },
  //     {
  //       image_url:
  //         "https://images.unsplash.com/photo-1512716679859-da19b4af9c38?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80",
  //       title: "ต้นกก",
  //       price: "132",
  //     },
  //     {
  //       image_url:
  //         "https://images.unsplash.com/photo-1545239705-1564e58b9e4a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80",
  //       title: "กอหญ้า",
  //       price: "532",
  //     },
  //   ],
  // }),
  middleware: "auth",
  computed: {
    ...mapGetters("product", {
      recommends: "items",
      spotted: "spotted",
      airpurifier: "airpurifier",
      ornamental: "ornamental",
      auspicious: "auspicious",
      fertilizer: "fertilizer",
    }),
  },
  methods: {
    ...mapActions("product", {
      fetch: "recommend",
      fetchByCat: "fetchByCat",
    }),
    showAlert() {
      // Use sweetalert2
      this.$swal("Hello Vue world!!!");
    },
  },
  async created() {
    await this.fetch();
    //load by id and custome name
    await this.fetchByCat({ category_id: 1, name: "spotted" });
    await this.fetchByCat({ category_id: 2, name: "airpurifier" });
    await this.fetchByCat({ category_id: 3, name: "ornamental" });
    await this.fetchByCat({ category_id: 4, name: "auspicious" });
    await this.fetchByCat({ category_id: 5, name: "fertilizer" });
  },

  metaInfo() {
    return { title: this.$("shop") };
  },
};
</script>
<style>
.product-card {
  max-width: 300px;
  background-color: #fff;
  box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.1);
  background-position: center;
  overflow: hidden;
  position: relative;
  margin: 10px auto;
  cursor: pointer;
  border-radius: 10px;
}

.product-card img {
  transition: all linear 0.25s;
}

.product-card .product-name {
  position: absolute;
  left: 30px;
  bottom: 105px !important;
  font-size: 30px;
  color: #fff;
  text-shadow: 0px 0px 20px rgba(0, 0, 0, 0.5);
  font-weight: bold;
  transition: all linear 0.25s;
}

.product-card .button-card {
  position: absolute;
  bottom: 30px;
  right: 30px;
  color: #fff;
  transition: all linear 0.25s;
}

.price {
  font-size: 20px !important;
}

.product-card .price {
  position: absolute;
  bottom: 80px;
  left: 30px;
  color: #fff;
  font-size: 30px;
  transition: all linear 0.25s;
}

.product-card .button-card {
  margin: 5px;
}

.product-card:hover img {
  transform: scale(1.1);
  filter: grayscale(30%) blur(1px) !important;
}

.product-card:hover .product-name {
  bottom: 110px !important;
}

.product-card:hover .price {
  bottom: 90px;
}

.product-card:hover .button-card {
  right: 40px;
}

.nopadding {
  padding: 0 !important;
  margin: 0 !important;
}

.b-red:hover {
  border-color: red !important;
  background-color: red !important;
  color: white;
}

.b-blue:hover {
  border-color: #86b6c9 !important;
  background-color: #86b6c9 !important;
  color: white;
}

.t-red {
  color: red !important;
}

.clearlink {
  color: black;
}

.clearlink:hover {
  color: grey;
}
</style>
