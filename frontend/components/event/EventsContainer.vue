<template>
  <v-card>
    <v-list-item v-for="event in this.$parent.events" :key="event.id" two-line>
      <v-list-item-content>
        <h4>{{ event.name }}</h4>
      </v-list-item-content>
      <v-btn class="mx-2" small fab dark color="cyan" @click="$emit('set', event)">
        <v-icon>mdi-pencil</v-icon>
      </v-btn>
      <v-btn class="mx-2" small fab dark color="pink" @click="removeEvent(event.id)">
        <v-icon>mdi-minus</v-icon>
      </v-btn>
    </v-list-item>
  </v-card>
</template>

<script>
export default {
  methods: {
    removeEvent(id) {
      this.$axios
        .delete(`/events/${id}`)
        .then((data) => {
          const events = this.$parent.events.filter((l) => l.id !== id)
          this.$parent.events = events
        })
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>