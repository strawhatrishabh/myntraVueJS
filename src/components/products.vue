<template>
  <div class="col-sm-9">
      <div
        v-infinite-scroll="loadMore"
        infinite-scroll-disabled="busy"
        infinite-scroll-distance="10"
      >
    <div class="row" style="margin-right: 15px;">
        <div
          class="col-3"
          v-for="(productItems, index) in data"
          :key="index"
          style="margin-bottom: 10px;"
        >
          <div class="card">
            <img class="card-img-top" alt="Card image cap" :src="productItems.image" />
            <div class="card-body">
              <p class="card-title" style="font-size: 14px; font-weight: 500;">{{productItems.name}}</p>
              <p
                class="card-text"
                style="font-size: 14px; font-weight: 600;"
              >Rs. {{productItems.price}}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import infiniteScroll from "vue-infinite-scroll";
import axios from "axios";

export default {
  props: { productData: Object, filterOptions: Array },
  directives: { infiniteScroll },
  data() {
      return {
          data: [],
          busy: false,
          count: 1
      }
  },
  watch: {
      filterOptions() {
          console.log("wfrwf");
          this.data.push(this.productData.result.products);
      }
  },
  mounted() {
      for(var i = 0; i < this.productData.result.products.length; i++) {
          this.data.push(this.productData.result.products[i]);
      }
    console.log(this.data);
  },
  methods: {
    loadMore: function() {
      this.busy = true;
      this.count++

      axios.get("https://v2pim.greenhonchos.com/pim/pimresponse.php/?service=category&store=1&url_key=men-topwear-t-shirt&page="+ this.count +"&count=15&sort_by=&sort_dir=desc&filter=" + this.filterOptions).then((responseResult_product_data) => {
          console.log(responseResult_product_data.data.result.products);
          for(var i = 0; i < responseResult_product_data.data.result.products.length; i++) {
                this.data.push(responseResult_product_data.data.result.products[i]);
            }
          this.busy = false;
      })
    }
  }
};
</script>

<style>
</style>