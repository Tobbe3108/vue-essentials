<template>
  <transition name="fade">
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label class="font-weight-bold mr-2" for="formMax">Max</label>
        <input
          id="formMax"
          type="text"
          class="form-control mx-2 text-center"
          style="width: 60px"
          v-model="maxAmount"
          @change="$parent.$emit('update:maximum', maxAmount)"
        />
        <input
          type="range"
          class="custom-range"
          min="1"
          max="150"
          v-model="maxAmount"
          @input="$parent.$emit('update:maximum', maxAmount)"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data() {
    return {
      maxAmount: 99
    };
  },
  props: ["sliderStatus"],
  computed: {
    sliderState() {
      return this.sliderStatus ? "d-flex" : "d-none";
    }
  }
};
</script>

<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.25s ease-in-out;
  -webkit-transition: all 0.25s ease-in-out;
  -moz-transition: all 0.25s ease-in-out;
  -ms-transition: all 0.25s ease-in-out;
  -o-transition: all 0.25s ease-in-out;
}
</style>