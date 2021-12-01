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

  created() {
    document.body.addEventListener('click', this.deselect)
  },

  beforeDestroyed() {
    document.body.removeEventListener('click', this.deselect)
  },

  methods: {
    select(el) {
      console.log('selectedParcel', el)
      this.selectedParcel = el
    },

    deselect() {
      this.selectedParcel = null
    }
  }
}
</script>

<style lang="scss" scoped>

.shipments {
  max-width: 1024px;
  margin: 0 auto;
  padding: 1rem;
}
</style>