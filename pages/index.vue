<template>
  <div>
    <h1>Events</h1>
    <EventCard
    v-for="(event,index) in events"
    :event="event"
    :key="index"
    :data-index="index"/>
  </div>
</template>

<script>
import EventCard from "@/components/EventCard.vue";
import { mapState } from "vuex";

export default {
  components: {
    EventCard
  },
  head() {
    return {
      title: "Events Listing"
    };
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch("events/fetchEvents");
    } catch (e) {
      error({
        statusCode: 503,
        message: "Can not fetch data at the moment. Please try again later."
      });
    }
  },
  computed: mapState({
    events: state => state.events.events
  })
};
</script>
