<template>
  <div class="shipments">
    <slot v-bind="{select, selectedParcel}"></slot>
  </div>
</template>

<script>
export default {
  name: 'shipments',

  data() {
    return {
      selectedParcel: null
    }
  },

  methods: {
    select(el) {
      console.log('selectedParcel', el)
      this.selectedParcel = el;
    },
  }
}
</script>