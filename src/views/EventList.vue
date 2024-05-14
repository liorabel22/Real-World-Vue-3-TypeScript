<template>
  <h1>Events for Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService'

import { type EventItem } from '@/types'

export default defineComponent({
  name: 'EventList',
  components: {
    EventCard
  },
  data() {
    return {
      events: [] as EventItem[]
    }
  },
  computed: {
    firstEvent(): EventItem {
      return this.events[0]
    }
  },
  created() {
    EventService.getEvents()
      .then((response) => {
        this.events = response.data
      })
      .catch((error) => {
        console.log(error)
      })
  },
  methods: {
    addEvent(newEvent: EventItem) {
      this.events.push(newEvent)
    },
    secondEvent(): EventItem {
      return this.events[1]
    }
  }
})
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
