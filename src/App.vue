<template>
  <div class="page">
    <shipments v-slot="{select, selectedParcel}">
      <parcel
        v-for="item in shipments"
        :item="item"
        :key="item.id"
        :selectedParcel="selectedParcel"
        @select-parcel="select($event)"
      />
    </shipments>
    <!--
    <aside>
      <selector v-model="selectedIndex" v-slot="slotData">
        <list :items="items">
          <template #list-title>
            <div class="list-title">Delivery method</div>
          </template>
          <template #list-body="{ item }">
            <list-item-simple :item="item" :selected="selectedIndex === item.index" @click="slotData.toggleSelect(item.index)" />
          </template>
        </list>
      </selector>
    </aside>
    -->
  </div>
</template>

<script>

import shipments from './components/shipments.vue'
import parcel from './components/parcel.vue'

import { mapState } from 'vuex'


export default {
  name: 'App',

  components: {
    shipments,
    parcel,
    //list,
    //listItemSimple,
    //selector
  },

  data() {
    return {
      selectedIndex: -1,
      items: [
        {value: 1, title: 'stadnard'},
        {value: 2, title: 'courier collection'},
        {value: 3, title: 'parcel drop off'},
        {value: 4, title: 'parcel drop off'}
      ],
    }
  },

  computed: {
    ...mapState(['shipments'])
  },

  methods: {
    onClick(e) {
      console.log(e)
    }
  }
}
</script>

<style lang="scss" scoped>
</style>