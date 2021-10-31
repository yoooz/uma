<template>
  <v-container>
    <v-row>
      <v-col>
        <v-row v-for="uma in umas" :key="uma.name">
          <v-col style="flex-grow: 0.13; text-align: right">
            {{ uma.rank }}
          </v-col>
          <v-col style="flex-grow: 1"> {{ uma.name }} </v-col>
          <v-col style="flex-grow: 5; display: flex">
            <div v-bind:style="{ width: uma.ran + '%' }"></div>
            {{ uma.index }}
            <v-img
              :src="require('@/assets/img/uma.png')"
              max-width="20"
              max-height="20"
            >
            </v-img>
          </v-col>
          <div style="background-color: white; height: 1px; width: 100%"></div>
        </v-row>
        <div
          style="
            background-color: white;
            position: absolute;
            height: 92%;
            width: 5px;
            top: 10px;
            right: 150px;
          "
        ></div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import umas from '../assets/json/umas.json'

const GOAL_LINE = 99
const SPEED = 10
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
    run() {
      const notGoald = this.umas.filter((uma) => uma.rank === ' ')
      const dash = Math.floor(Math.random() * notGoald.length)
      const targetUmaName = notGoald[dash].name

      const targetUmaIndex = this.umas.findIndex(
        (uma) => uma.name === targetUmaName
      )

      if (targetUmaIndex < 0) {
        return
      }

      const ran = this.umas[targetUmaIndex].ran + SPEED

      this.umas[targetUmaIndex].ran = ran > GOAL_LINE ? GOAL_LINE : ran

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
