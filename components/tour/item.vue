<template>
  <div class="tour">
    <nuxt-link class="tour-link" :to="'/results/' + tour.slug">
      <h1 class="tour-title">{{tour.title}}</h1>
      <p class="tour-text">from {{tour.totalPrice.min}} $ per person</p>
      <div class="tour-images"></div>
    </nuxt-link>
    <!-- <nuxt-link :to="'/results/' + slug" class="tour-link">
      <h1 class="tour-title">{{title}}</h1>
      <p class="tour-text">from {{minPrice}} $ per person</p>
      <div class="tour-images"></div>
    </nuxt-link> -->
  </div>
</template>

<script>
export default {
  name: "tour",
  props: {
    tour: {
      type: Object,
      required: true
    }
  }
};
</script>

<style>
.tour {
  margin: 2rem 0;
  width: 90%;
  background-color: #fff;
  border-radius: 5px;
  padding: 2rem;
  border: 1px solid #e5e5e5;
  box-shadow: 2px 4px 2px 4px #e5e5e5;
}
.tour-link {
  text-decoration: none;
  color: black;
}

.tour-img {
  height: 30px;
  width: 30px;
}

@media screen and (min-width: 768px) {
  .tour {
    width: 40rem;
  }
}
</style>