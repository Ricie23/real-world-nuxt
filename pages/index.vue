<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" :data-index="index"/>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: "IndexPage",
  head() {
    return {
      title: "Event Listing",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "where you can find all the events.",
        },
      ],
    };
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch("events/fetchEvents");
    } catch (e) {
      error({ statusCode: 503, message: "unable to fetch events" });
    }
  },
  computed: mapState({
    events: (state) => state.events.events,
  }),
};
</script>
