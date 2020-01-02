<template>
  <div class="eventItemList">
    <div v-for="event in events" :key="event.eventListID">
      <EventItem
        :eventListID="event.eventListID"
        :eventId="event.eventId"
        :price="event.price"
        :quantity="event.quantity"
        :inclusive="event.inclusive"
        @totalTickets="totalTickets"
        @events-quantity-total="quantityChanged"
      />
    </div>
    <p>{{sumTickets}}</p>
  </div>
</template>

<script>
import EventItem from "./EventItem.vue";

export default {
  name: "EventItemList",
  components: {
    EventItem
  },
  props: ["events"],
  data() {
    return {
      sumTickets: 0
    };
  },
  methods: {}
};
</script>

<style>
</style>
