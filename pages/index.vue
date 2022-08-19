<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" :data-index="index"/>
  </div>
</template>

<script>
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
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get("http://localhost:3000/events");
      return {
        events: data,
      };
    } catch (e) {
      error({ statusCode: 503, message: "unable to fetch events" });
    }
  },
};
</script>
