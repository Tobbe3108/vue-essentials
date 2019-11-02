<template>
  <transition-group tag="div" @beforeEnter="beforeEnter" @enter="enter" @leave="leave">
    <div
      class="row d-flex mb-3 align-items-center"
      v-for="(item, index) in productsToShow"
      :key="item.id"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button class="btn btn-info" @click="$parent.$emit('add', item)">+</button>
      </div>
      <div class="col-4">
        <img class="img-fluid d-block" :src="item.image" :alt="item.image_title" />
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.name }}</h3>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right">
          <Price :value="Number(item.price)"></Price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";

export default {
  name: "product-list",
  components: { Price },
  props: ["products", "maximum"],
  methods: {
    beforeEnter(el) {
      el.className = "d-none";
    },
    enter(el) {
      var delay = el.dataset.index * 50;
      setTimeout(function() {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeInRight";
      }, delay);
    },
    leave(el) {
      var delay = el.dataset.index * 50;
      setTimeout(function() {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeOutLeft";
      }, delay);
    }
  },
  computed: {
    productsToShow() {
      return this.products.filter(item => item.price <= this.maximum);
    }
  }
};
</script>