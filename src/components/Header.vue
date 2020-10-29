<template>
  <div class="header">
    <nav class="navbar navbar-expand-lg shadow-sm bg-white rounded">
      <a class="navbar-brand" style="margin-left: 2%;">
        <img src="@/assets/images/logo.png" alt="V2 Kart" title="V2 Kart" />
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item" v-for="(category, index) in categoryLabels" :key="index">
            <a class="desktop-main" href="#">{{category.name}}</a>
          </li>
        </ul>
        <div class="desktop-query" data-reactid="693">
          <input
            placeholder="Search for products, brands and more"
            class="desktop-searchBar"
            value
            data-reactid="694"
          />
          <a class="desktop-submit" data-reactid="695" style="color: black;">
            <span class="myntraweb-sprite desktop-iconSearch sprites-search" data-reactid="696">
              <svg
                width="1em"
                height="1em"
                viewBox="0 0 16 16"
                class="bi bi-search"
                fill="currentColor"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M10.442 10.442a1 1 0 0 1 1.415 0l3.85 3.85a1 1 0 0 1-1.414 1.415l-3.85-3.85a1 1 0 0 1 0-1.415z"
                />
                <path
                  fill-rule="evenodd"
                  d="M6.5 12a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zM13 6.5a6.5 6.5 0 1 1-13 0 6.5 6.5 0 0 1 13 0z"
                />
              </svg>
            </span>
          </a>
        </div>
      </div>
      <div class="right-menu">
        <span>
          <svg
            width="1em"
            height="1em"
            viewBox="0 0 16 16"
            class="bi bi-person"
            fill="currentColor"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M10 5a2 2 0 1 1-4 0 2 2 0 0 1 4 0zM8 8a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm6 5c0 1-1 1-1 1H3s-1 0-1-1 1-4 6-4 6 3 6 4zm-1-.004c-.001-.246-.154-.986-.832-1.664C11.516 10.68 10.289 10 8 10c-2.29 0-3.516.68-4.168 1.332-.678.678-.83 1.418-.832 1.664h10z"
            />
          </svg>
        </span>
        <br />
        <span class="desktop-userTitle">Profile</span>
      </div>
      <div class="right-menu">
        <span>
          <svg
            width="1em"
            height="1em"
            viewBox="0 0 16 16"
            class="bi bi-bookmark"
            fill="currentColor"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v13.5a.5.5 0 0 1-.777.416L8 13.101l-5.223 2.815A.5.5 0 0 1 2 15.5V2zm2-1a1 1 0 0 0-1 1v12.566l4.723-2.482a.5.5 0 0 1 .554 0L13 14.566V2a1 1 0 0 0-1-1H4z"
            />
          </svg>
        </span>
        <br />
        <span class="desktop-userTitle">WishList</span>
      </div>
      <div class="right-menu">
        <span>
          <svg
            width="1em"
            height="1em"
            viewBox="0 0 16 16"
            class="bi bi-bag"
            fill="currentColor"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M8 1a2.5 2.5 0 0 0-2.5 2.5V4h5v-.5A2.5 2.5 0 0 0 8 1zm3.5 3v-.5a3.5 3.5 0 1 0-7 0V4H1v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V4h-3.5zM2 5v9a1 1 0 0 0 1 1h10a1 1 0 0 0 1-1V5H2z"
            />
          </svg>
        </span>
        <br />
        <span class="desktop-userTitle">Cart</span>
      </div>
    </nav>
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item">
          <a href="/" class="router-link-active">Home</a>
        </li>
        <li class="breadcrumb-item">
          <a href="/category/men-topwear.html" class>Topwear</a>
        </li>
        <li class="breadcrumb-item active">T Shirts</li>
      </ol>
    </nav>
  </div>
</template>

<script>
export default {
  props: { categoryLabels: Object }
};
</script>

<style>
.right-menu {
  padding-right: 20px;
}
.desktop-userTitle {
  color: #000;
  /* position: absolute; */
  bottom: 4px;
  left: 1px;
  font-size: 12px;
  font-weight: 500;
  display: inline-block;
  /* padding-top: 10px; */
  line-height: 6px;
  font-weight: 600;
}
.desktop-main {
  padding: 0 10px 28px;
  text-align: center;
  text-decoration: none;
  font-size: 14px;
  letter-spacing: 0.3px;
  color: #282c3f;
  border-bottom: none;
  -webkit-transition: left 0.2s ease-out, width 0.2s ease-out;
  transition: left 0.2s ease-out, width 0.2s ease-out;
  font-weight: 500;
  text-transform: uppercase;
  font-weight: 700;
}
.desktop-query {
  width: 465px;
  float: right;
  line-height: 0;
  margin: 20px 20px 20px 60px;
  position: relative;
}
.desktop-query > input.desktop-searchBar {
  display: inline-block;
  float: left;
  font-size: 14px;
  height: 20px;
  line-height: 24px;
  width: 95%;
  color: #696e79;
  -webkit-box-sizing: content-box;
  box-sizing: content-box;
  padding: 8px 10px 10px;
  margin: 0;
  outline: 0;
  border: 1px solid #f5f5f6;
  border-radius: 0 4px 4px 0;
  border-left: 0;
  background: #f5f5f6;
}
a.desktop-submit {
  -webkit-box-sizing: content-box;
  box-sizing: content-box;
  display: inline-block;
  height: 28px;
  width: 40px;
  text-align: center;
  padding: 8px 0 2px;
  background: #f5f5f6;
  border: 1px solid #f5f5f6;
  border-right: none;
  border-radius: 4px 0 0 4px;
  position: absolute;
  left: -41px;
}
.desktop-wishlist {
  margin: 0 55px 0 10px;
}
.desktop-cart,
.desktop-wishlist {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  text-decoration: none;
  position: relative;
}
.desktop-iconWishlist {
  left: 11px;
}
.desktop-iconBag,
.desktop-iconWishlist {
  margin: 8px 0 0;
  position: absolute;
  bottom: 14px;
}
.sprites-headerWishlist {
  width: 22px;
  height: 22px;
  background-position: -320px -56px;
}
.breadcrumb {
  border-radius: inherit;
  background-color: snow;
  padding: 0.5rem 2rem;
  margin-bottom: 0px;
}
.breadcrumb li {
  font-size: 14px;
}
.breadcrumb li.breadcrumb-item a {
  color: #000;
}
.header {
    text-align: center;
}
</style>