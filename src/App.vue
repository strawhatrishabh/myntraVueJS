<template>
  <div id="app">
    <Header :categoryLabels="responseResult_menu_data" />
      <router-view />
  </div>
</template>

<script>
import axios from "axios";
import Header from "@/components/Header.vue";

export default {
  name: "App",
  components: {
    Header,
  },
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
  mounted() {
    axios
      .get(this.api_url_menu_data)
      .then(response => {
        this.responseResult_menu_data = response.data.result;
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
      // this.$router.push('/category/men-topwear-t-shirt&filter=')
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.borderClass {
  border-right: 1px solid !important;
  border-top: 1px solid;
  border-color: gainsboro !important;
}
.title-container {
  margin: 10px 0 5px 25px;
}
.title-title {
  font-weight: 700;
  display: inline-block;
  text-overflow: ellipsis;
  vertical-align: top;
  overflow: hidden;
  white-space: nowrap;
  font-size: 16px;
  margin: 0;
  max-width: 400px;
  color: #282c3f;
  text-transform: capitalize;
}
.title-count {
  font-size: 16px;
  color: #878b94;
}
.header-container {
  position: relative;
  border-right: none !important;
  padding-top: 0;
}
.vertical-filters-filters {
  padding-top: 20px;
  padding-bottom: 15px;
  padding-left: 25px;
  border-bottom: 1px solid #e9e9ed;
  position: relative;
  border-right: 1px solid #edebef !important;
}
.header-title {
  font-weight: 700;
}
</style>
