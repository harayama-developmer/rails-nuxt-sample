<template>
  <v-flex>
    <v-card>
      <v-card-text>
        <v-form ref="form" @submit.prevent>
          <v-text-field v-model="name" label="name" ref="nameInput" @keyup.enter="addEvent" />
        </v-form>
        <v-card-actions>
          <v-btn class="mx-2" fab dark color="indigo" @click="addEvent">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card-text>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  data() {
    return {
      name: '',
    }
  },
  methods: {
    addEvent() {
      this.$axios
        .$post('/events', { event: { name: this.name }})
        .then((data) => {
          this.$parent.events.push(data)
          this.name = ''
          this.$refs.nameInput.focus()
        })
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>
