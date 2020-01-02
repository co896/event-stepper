<template>
  <div class="eventList">
    <div v-for="event in events" :key="event.eventListID">
      <div class="eventItem">
        <div class="row row justify-content-between">
          <div id="description" class="col-12 col-lg-10 col-md-9 col-sm-8">
            <p>Event: {{ event.eventId }}</p>
            <p>£{{ event.price }}</p>
          </div>
          <div id="selectTickets" class="col-6 col-lg-2 col-md-3 col-sm-4">
            <button
              type="button"
              class="btn btn-info"
              @click="$emit('minus', event)"
              v-if="event.quantity > 0"
            >-</button>
            <button type="button" class="btn btn-info" v-else>-</button>
            <span>{{event.quantity}}</span>
            <button type="button" class="btn btn-info" @click="$emit('add', event)">+</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "EventList",
  props: {
    events: {
      type: Array
    },
    tickets: {
      type: Number
    }
  },
  data() {
    return {};
  },
  methods: {}
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
