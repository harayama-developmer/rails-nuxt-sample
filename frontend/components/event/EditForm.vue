<template>
  <v-flex>
    <v-card>
      <v-card-text>
        <v-form ref="form" @submit.prevent>
          <v-text-field v-model="name" label="name" />
        </v-form>
        <v-card-actions>
          <v-btn class="mx-2" fab dark color="teal" @click="editEvent">
            <v-icon dark>mdi-pencil</v-icon>
          </v-btn>
        </v-card-actions>
        <v-card-actions>
          <v-btn color="secondary" @click="cancel">戻る</v-btn>
        </v-card-actions>
      </v-card-text>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  props: {
    event: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      id: this.event.id,
      name: this.event.name,
    }
  },
  methods: {
    editEvent() {
      this.$axios
        .$put(`/events/${this.id}`, {
          event: {
            name: this.name,
          }
        })
        .then((data) => {
          const events = this.$parent.events.map((l) => {
            return l.id === this.id ? data : l
          })
          this.$parent.events = events
          this.$emit('set')
        })
        .catch((err) => {
          console.log(err)
        })
    },
    cancel() {
      this.$parent.editTargetEvent = ''
    }
  }
}
</script>