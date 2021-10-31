<template>
  <v-container>
    <v-row>
      <v-col>
        <v-row v-for="uma in umas" :key="uma.name">
          <v-col style="flex-grow: 0.2"> {{ uma.rank }} </v-col>
          <v-col style="flex-grow: 1"> {{ uma.name }} </v-col>
          <v-col style="flex-grow: 5; display: flex">
            <div v-bind:style="{ width: uma.ran + '%' }"></div>
            馬
          </v-col>
        </v-row>
        <div
          style="
            background-color: white;
            position: absolute;
            height: 92%;
            width: 5px;
            top: 10px;
            right: 200px;
          "
        ></div>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-btn @click="run">START!!</v-btn>
    </v-row>
  </v-container>
</template>

<script>
import umas from '../assets/json/umas.json'

const GOAL_LINE = 99
const SPEED = 40
export default {
  data() {
    return {
      umas,
    }
  },
  created() {
    setInterval(() => {
      this.run()
    }, 100)
  },
  methods: {
    start() {
      // this.isRunning = true
    },
    run() {
      const dash = Math.floor(Math.random() * this.umas.length)

      const ran = this.umas[dash].ran + SPEED
      this.umas[dash].ran = ran > GOAL_LINE ? GOAL_LINE : ran

      const finishIndex = this.umas.findIndex(
        (uma) => uma.ran >= GOAL_LINE && uma.rank === ' '
      )

      if (finishIndex < 0) {
        return
      }

      const goald = this.umas.filter(
        (uma) => uma.ran >= GOAL_LINE && uma.rank !== ' '
      )
      this.umas[finishIndex].rank = `${goald.length + 1}着`
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
