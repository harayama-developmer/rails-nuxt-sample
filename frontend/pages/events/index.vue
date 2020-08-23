<template>
  <div class="home">
    <template v-if="editTargetEvent">
      <EditForm :event="editTargetEvent" @set="editingEvent" />
    </template>
    <template v-else>
      <NewForm class="mb-5"/>
      <EventsContainer @set="editingEvent" />
    </template>
  </div>
</template>

<script>
import EventsContainer from '~/components/event/EventsContainer.vue'
import NewForm from '~/components/event/NewForm.vue'
import EditForm from '~/components/event/EditForm.vue'

export default {
  components: {
    EventsContainer,
    NewForm,
    EditForm
  },
  data() {
    return {
      events: [],
      editTargetEvent: ''
    }
  },
  async asyncData({ $axios }) {
    const data = await $axios.$get('/events')
    return { events: data }
  },
  methods: {
    editingEvent(event = '') {
      this.editTargetEvent = event
    }
  }
}
</script>

<style>
</style>