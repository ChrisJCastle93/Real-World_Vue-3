<template>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue';
import EventService from '@/services/EventService';

// import axios from 'axios';

export default {
  name: 'EventList',
  props: ['page'], // <---- receive the param as a prop, the current page
  components: {
    EventCard,
  },
  data() {
    return {
      events: null,
    };
  },
  created() {
    EventService.getEvents(2, this.page) // <---- 2 events per page, and current page
      .then((response) => {
        // eslint-disable-next-line no-console
        console.log(response.data);
        this.events = response.data;
      })
      .catch((error) => {
        throw new Error(error);
      });
  },
};
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
