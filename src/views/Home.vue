<template>
  <Filters :filterData="responseResult_product_data" />
</template>

<script>
import axios from "axios";
import Filters from "@/components/Filters.vue";
export default {
    data() {
    return {
      active: false,
      api_url_menu_data:
        "https://v2pim.greenhonchos.com/pim/pimresponse.php/?service=menu&store=1",
      responseResult_menu_data: {},
      api_url_product_data:
        "https://v2pim.greenhonchos.com/pim/pimresponse.php/?service=category&store=1&url_key=men-topwear-t-shirt&page=1&count=15&sort_by=&sort_dir=desc&filter=",
      responseResult_product_data: {}
    };
  },
  components: {
      Filters
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

}
</script>