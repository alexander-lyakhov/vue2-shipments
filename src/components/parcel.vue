<template>
  <div class="parcel" :class="{selected: isSelected}" @click.stop="select">
    <div class="parcel-item">
      <div class="parcel-caption">
        <span class="title">{{ item.parcelContents }}</span>
        <span class="actions">
          <a class="actions-btn actions-btn-edit" href="#">
            <svg viewBox="0 0 24 24">
              <path fill="currentColor" d="M14.06,9L15,9.94L5.92,19H5V18.08L14.06,9M17.66,3C17.41,3 17.15,3.1 16.96,3.29L15.13,5.12L18.88,8.87L20.71,7.04C21.1,6.65 21.1,6 20.71,5.63L18.37,3.29C18.17,3.09 17.92,3 17.66,3M14.06,6.19L3,17.25V21H6.75L17.81,9.94L14.06,6.19Z" />
            </svg>
          </a>
          <a class="actions-btn actions-btn-delete" href="#">
            <svg viewBox="0 0 24 24">
              <path fill="currentColor" d="M9,3V4H4V6H5V19A2,2 0 0,0 7,21H17A2,2 0 0,0 19,19V6H20V4H15V3H9M7,6H17V19H7V6M9,8V17H11V8H9M13,8V17H15V8H13Z" />
            </svg>
          </a>
        </span>
      </div>
      <div class="parcel-body">
        <table>
          <tr>
            <th class="name">{{ fullName }}</th>
            <th class="weight">Wight</th>
            <th class="delivery">Delivery Service</th>
            <th class="cover">Cover</th>
            <th class="proof">Proof of delivery</th>
          </tr>
          <tr>
            <td>
              <div class="postcode">{{ item.recipientDetails.postcode }}</div>
              <div class="delivery">Parcelshop drop off</div>
            </td>
            <td>1kg - 2kg</td>
            <td>Standard</td>
            <td>Free cover up to ?15</td>
            <td>Not included</td>
          </tr>
        </table>
      </div>
      <div class="parcel-footer">
        <img src="../assets/csv.svg" />
        <span class="price">
          {{ item.parcelValuePence / 100 }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'parcel',

  props: {
    item: {
      type: Object,
      default: () => {}
    },

    selectedParcel: {
      type: Object,
      default: null
    }
  },

  data() {
    return {}
  },

  computed: {
    isSelected() {
      if (this.selectedParcel) {
        return this.selectedParcel?.$el === this.$el
      }
      return false
    },

    fullName() {
      return this.item.recipientDetails?.firstName + ' ' + this.item.recipientDetails?.lastName
    }
  },

  methods: {
    select() {
      console.log('select', this.$el)
      this.$emit('select-parcel', this);
    }
  }
}
</script>

<style lang="scss" scoped>
.parcel {
  color: map-get($parcel, fc);
  background: map-get($parcel, bg);
  border-radius: 6px;
  box-shadow: 0 4px 8px #00000060;
  margin: 0 0 2rem;
  padding: 5px;
  overflow: hidden;
  position: relative;
  cursor: pointer;

  &.selected {
    background: #e09000;
  }

  &-caption {
    $bg-header: map-get($parcel-header, bg);

    font-size: 1.25rem;
    color: map-get($parcel-header, fc);
    background: $bg-header;
    background: linear-gradient(to bottom, lighten($bg-header, 12%), darken($bg-header, 5%));
    border-bottom: 2px solid $fc-middle;
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-align: left;
    text-transform: capitalize;
    letter-spacing: 1px;
    text-shadow: 1px 1px 0px #000;
    padding: .5rem .5rem .5rem 1rem;

    .actions {
      &-btn {
        border: 1px solid transparent;
        display: inline-block;
        margin: 0 .25rem;
        padding: .25rem;

        &:hover {
          border: 1px solid #e0e0e0;
          border-radius: 4px;
        }

        svg {
          color: #c0d0e0;
          width: 32px;
          height: 32px;
        }
      }
    }
  }

  &-body {
    background: map-get($parcel-body, bg);
    padding: .75rem 0;

    table {
      font-size: 1rem;
      width: 100%;
      border-collapse: collapse;

      tr {
        th, td {
          text-align: left;
          padding: .25rem 1rem;
        }

        th {
          font-weight: bold;
          color: $fc-title;
        }

        td {
          vertical-align: top;
        }

        .postcode, .delivery {
          padding: .5rem 0;
        }
      }
    }
  }

  &-footer {
    font-size: 1.75rem;
    color: map-get($parcel-footer, fc);
    background: map-get($parcel-footer, bg);
    display: flex;
    justify-content: space-between;
    padding: .75rem 1rem;
  }
}
</style>
