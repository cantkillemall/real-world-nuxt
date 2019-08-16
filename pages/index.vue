<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard'

export default {
  components: {
    EventCard
  },
  head() {
    return {
      title: 'Event Listing'
    }
  },
  computed: mapState({
    // eslint-disable-next-line prettier/prettier
    events: state => state.events.events
  }),
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Pleas try again.'
      })
    }
  }
}
</script>
