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
              <div>
            <input type="checkbox" class="form-check-input" :id="indexOptions" @click="applyFilter(filterOptions)" />
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
            <!-- <span data-colorhex="black" class="colour-label colour-colorDisplay" style="background-color: rgb(54, 69, 79);"></span> -->
            <label
              class="form-check-label"
              :for="indexOptions"
              style="font-size: 14px;"
            >{{filterOptions.value}}</label>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <Products :productData="responseResult_product_data" :filterOptions="axiosFinalFilterOptions" />
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
        "https://v2pim.greenhonchos.com/pim/pimresponse.php/?service=category&store=1&url_key=men-topwear-t-shirt&page=1&count=15&sort_by=&sort_dir=desc&filter=",
      selectedFiltersValueKey: [],
      selectedFilterCode: [],
      axiosFinalFilterOptions: [],
    //   api_url_product_data:
    //     "https://v2pim.greenhonchos.com/pim/pimresponse.php/?service=category&store=1&url_key=men-topwear-t-shirt&page=1&count=15&sort_by=&sort_dir=desc&filter=",
      responseResult_product_data: {}
    };
  },
  components: {
    RangeSlider,
    Products
  },
  mounted() {
      axios
      .get(this.api_url_product_data)
      .then(response => {
        this.responseResult_product_data = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
      applyFilter(filterOptions) {
          console.log(filterOptions);
          this.selectedFiltersValueKey.push(filterOptions.value_key);
          this.selectedFilterCode.push(filterOptions.code);
          this.axiosFinalFilterOptions.push(this.selectedFilterCode + "~" + this.selectedFiltersValueKey);
          if(this.selectedFiltersValueKey.length > 1) {
              this.axiosFinalFilterOptions = [];
              for(var i = 0; i < this.selectedFiltersValueKey.length; i++) {
                  this.axiosFinalFilterOptions.push(this.selectedFilterCode[i] + "~" + this.selectedFiltersValueKey[i])
              }
          }
          console.log(this.axiosFinalFilterOptions)
          axios.get(this.api_url_product_data + this.axiosFinalFilterOptions).then((responseFilteredProductData) => {
              this.responseResult_product_data = responseFilteredProductData.data;
              console.log(this.responseResult_product_data);
          }).catch((error) => {
              console.log(error);
          })
      }
  }
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