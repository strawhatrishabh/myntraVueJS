<template>
<div class="Filters">
<div class="title-container">
      <h1 class="title-title">Men T-shirts</h1>
      <span class="title-count">- {{responseResult_product_data.result.count}}</span>
    </div>
    <div class="row">
      <div class="col-3">
        <div class="vertical-filters-filters header-container borderClass">
          <span class="header-title">FILTERS</span>
        </div>
      </div>
    </div>
<div class="row">
  <div class="col-sm-3">
    <span>Checked names: {{ checkedNames }}</span>
      <range-slider
        class="slider"
        min="10"
        max="1000"
        step="10"
        v-model="sliderValue"
        style="display: none;"
      ></range-slider>
      <div
        class="vertical-filters"
        v-for="(filters,index) in filterData.result.filters"
        :key="index"
      >
        <span style="margin-left: 20px; font-weight: 700;">{{filters.filter_lable}}</span>
        <ul>
          <li v-for="(filterOptions,indexOptions) in filters.options" :key="indexOptions">
            <input type="checkbox" class="form-check-input" :id="indexOptions" :value="filterOptions" v-model="checkedNames">
            <svg
              width="1em"
              height="1em"
              viewBox="0 0 16 16"
              class="bi bi-circle-fill"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
              v-if="filters.filter_lable == 'Color'"
             v-bind:style="{ color: filterOptions.value_key}"
             style="border: 1px solid; border-radius: 10px; border-color: gainsboro;"
            >
              <circle cx="8" cy="8" r="8" />
            </svg>
            <label style="font-size: 14px;" class="form-check-label" for="jack">{{filterOptions.value}}</label>
            <!-- <input type="checkbox" id="john" value="John" v-model="checkedNames">
            <label for="john">John</label>
            <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
            <label for="mike">Mike</label> -->
            <br>
          </li>
        </ul>
      </div>
    </div>
    <Products :productData="responseResult_product_data" :filterOptions="queryStringFilters" />
  </div>
  </div>
</template>

<script>
import RangeSlider from "vue-range-slider";
import "vue-range-slider/dist/vue-range-slider.css";
import axios from "axios";
import Products from "@/components/products.vue";

export default {
  props: { filterData: Object },
  data() {
    return {
      sliderValue: [20, 70],
      api_url_product_data:
        "https://v2pim.greenhonchos.com/pim/pimresponse.php/?service=category&store=1&page=1&count=15&sort_by=&sort_dir=desc&url_key=",
      selectedFiltersValueKey: [],
      selectedFilterCode: [],
      axiosFinalFilterOptions: [],
      responseResult_product_data: {},
      checkedNames: [],
      queryStringFilters: []
    };
  },
  components: {
    RangeSlider,
    Products
  },
  mounted() {
    // console.log(this.filterData.result.filters);
      axios
      .get(this.api_url_product_data + this.$route.params.id)
      .then(response => {
        this.responseResult_product_data = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  },
  watch: {
    checkedNames() {
      if(this.checkedNames.length == 1) {
        this.$route.params.id = "men-topwear-t-shirt&filter=" + this.checkedNames[0].code + "~" + this.checkedNames[0].value;
        axios.get(this.api_url_product_data + this.$route.params.id).then((responseFilteredProductData) => {
          this.responseResult_product_data = responseFilteredProductData.data;
        })
        this.$router.push({name: 'Home', params: this.$route.params})
      } else {
          this.axiosFinalFilterOptions = [];
          this.queryStringFilters = [];
          for(var i = 0; i < this.checkedNames.length; i++) {
              this.axiosFinalFilterOptions.push(this.checkedNames[i].code + "~" + this.checkedNames[i].value)
          }
          this.axiosFinalFilterOptions.forEach((result) => {
            this.queryStringFilters.push(result)
          })
          this.queryStringFilters = this.queryStringFilters.toString().replace(/,/gi, "|");
          this.$route.params.id = "men-topwear-t-shirt&filter=" + this.queryStringFilters;
          axios.get(this.api_url_product_data + this.$route.params.id).then((responseFilteredProductData) => {
            this.responseResult_product_data = responseFilteredProductData.data;
          })
          this.$router.push({name: 'Home', params: this.$route.params})
      }
    }
  },
};
</script>

<style scoped>
.categories-container {
  position: relative;
}
.vertical-filters {
  border-right: 1px solid;
  border-bottom: 1px solid;
  border-color: gainsboro;
}
</style>