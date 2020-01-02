<template>
  <div class="eventItem">
    <div class="row row justify-content-between">
      <div id="description" class="col-12 col-lg-10 col-md-9 col-sm-8">
        <p>Event: {{ eventId }}</p>
        <p>£{{ price }}</p>
      </div>
      <div id="selectTickets" class="col-6 col-lg-2 col-md-3 col-sm-4">
        <button type="button" class="btn btn-info" @click="minus" v-if="quantity > 0">-</button>
        <button type="button" class="btn btn-info" v-else>-</button>
        <input v-model="myQuantity" @input="$emit('update:quantity', myQuantity)" />
        <button type="button" class="btn btn-info" @click="$parent.$emit('change', eventListID)">+</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "EventItem",
  props: {
    eventListID: {
      type: Number,
      default: 0
    },
    eventId: {
      type: String,
      default: "9999",
      required: false
    },
    price: {
      type: String,
      default: "0.00",
      required: true
    },
    quantity: {
      type: Number,
      default: 0,
      required: true
    },
    inclusive: {
      type: Boolean,
      default: false,
      required: false
    }
  },
  data() {
    return {
      myQuantity: 0
    };
  }
};
</script>

<style>
#description {
  padding-left: 2em;
}
#selectTickets span {
  margin: 1em;
}
</style>