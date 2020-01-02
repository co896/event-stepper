<template>
  <div class="eventBreakdown">
    <h5>{{ title }}</h5>
    <p>Tickets selected: {{tickets}}</p>
    <p>Discount: £{{ priceInfo.discount }}</p>
    <p>Booking fee: £{{ priceInfo.bookingFee }}</p>
    <p>Total price:£{{ priceInfo.totalPrice }}</p>

    <div id="error" v-if="!error">{{error}}</div>
  </div>
</template>

<script>
export default {
  name: "EventBreakdown",
  props: ["events", "tickets", "priceInfo"],
  data() {
    return {
      title: "Price breakdown",
      bookings: [],
      sumTotal: 0,
      ticketsTotal: 0,
      error: ""
    };
  }
};
</script>

<style>
.eventBreakdown {
  font-size: 0.75rem;
  background-color: #ccdadd;
  padding-top: 2rem;
}
.eventBreakdown p {
  margin: 10px 0;
}
</style>
