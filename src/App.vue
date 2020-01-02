<template>
  <div id="app" class="container">
    <div>
      <h5>Select which events you'd like to attend and how many tickets you need</h5>
    </div>
    <div>
      <h3>{{ title }}</h3>
      <EventList :events="events" @add="add" @minus="minus" />
    </div>
    <div>
      <EventBreakdown :events="events" :tickets="sumTickets" :priceInfo="priceData" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import EventList from "./components/EventList.vue";
import EventBreakdown from "./components/EventBreakdown.vue";

export default {
  name: "app",
  components: {
    EventList,
    EventBreakdown
  },
  data() {
    return {
      events: [],
      title: "Events",
      eventIndex: 0,
      sumTickets: 0,
      priceData: {},
      postURL: "http://curie.ticketlab.co.uk/api/calculateFees"
    };
  },
  mounted() {
    axios
      .get("./data/events.json")
      .then(
        response =>
          (this.events = response.data.map(item => {
            item.eventListID = this.eventIndex;
            this.eventIndex++;
            return item;
          }))
      )
      .catch(err => {
        this.error = err;
      });
  },
  methods: {
    add: function(event) {
      this.events.quantity = event.quantity++;
      this.sumTickets++;
      this.postData();
    },
    minus: function(event) {
      this.events.quantity = event.quantity--;
      this.sumTickets--;
      this.postData();
    },
    postData: function() {
      // send a POST request
      /*eslint no-console: ["error", { allow: ["warn", "error","log"] }] */
      console.log(this.events);
      let tickets = {
        tickets: this.events
      };
      console.log(tickets);
      axios
        .post(this.postURL, tickets)
        .then(function(response) {
          console.log(response);
          this.priceData = response.data;
        })
        .catch(err => {
          this.error = err;
        });
    }
  }
};
</script>

<style>
body {
  background-color: #ccdadd;
}
.container {
  background-color: #ffffff;
  padding: 0;
  max-width: 900px;
}
h3 {
  background-color: rgb(235, 235, 235);
  font-weight: 300;
  /* padding: 0.5rem; */
  padding: 0.5rem 1rem;
}
h5 {
  background-color: #ccdadd;
  margin: 0;
  padding-bottom: 0.3rem;
  font-weight: 300;
}
</style>
