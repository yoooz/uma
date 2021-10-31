<template>
  <v-container>
    <v-row class="rane" justify="center">
      <v-col v-for="uma in umas" :key="uma.name" class="flex">
        <div v-bind:style="{ height: uma.ran + '%' }"></div>
        {{ uma.name }}
      </v-col>
    </v-row>
    <v-row>
      <v-col v-for="uma in umas" :key="uma.name">
        {{ uma.rank }}
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-btn @click="run">START!!</v-btn>
    </v-row>
  </v-container>
</template>

<script>
import umas from '../assets/json/umas.json'

const GOAL_LINE = 80
const SPEED = 10
export default {
  data() {
    return {
      umas,
    }
  },
  methods: {
    start() {
      console.dir(this.umas.filter((element) => element.ran < GOAL_LINE))
      while (
        this.umas.filter((element) => element.ran < GOAL_LINE).length > 0
      ) {
        console.log('run')
        this.run()
        // setTimeout(this.run, 1000)
      }
    },
    run() {
      const dash = Math.floor(Math.random() * this.umas.length)

      const ran = this.umas[dash].ran + SPEED
      this.umas[dash].ran = ran > GOAL_LINE ? GOAL_LINE : ran

      const finishIndex = this.umas.findIndex(
        (uma) => uma.ran >= GOAL_LINE && uma.rank === ''
      )
      console.log(finishIndex)

      if (finishIndex < 0) {
        return
      }

      const goald = this.umas.filter(
        (uma) => uma.ran >= GOAL_LINE && uma.rank !== ''
      )
      this.umas[finishIndex].rank = `${goald.length + 1}`
    },
  },
}
</script>

<style scoped>
.rane {
  height: 80vh;
}

.flex {
  display: flex;
  flex-direction: column;
}
</style>
