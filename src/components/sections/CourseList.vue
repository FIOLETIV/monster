<template>
  <header>
    <h1>Vue Course Goals</h1>
  </header>
  <section id="user-goals">
    <h2>My course goals</h2>
    <input type="text" v-model="enteredGoalValue"/>
    <button @click="addGoal">Add Goal</button>
    <ul v-if="toggleTaskIsVisible">
      <li v-for="(goal, index) in goals" :key="goal" @click="removeGoal(index)">
        {{ goal }} - {{ index }}
      </li>
    </ul>
    <button @click="toggleTaskList">{{ buttonCaption }}</button>
<!--    <ul>-->
<!--      <li v-for="(value, key, index) in person">{{ k ey }}: {{ value }} - {{ index }}</li>-->
<!--    </ul>-->
  </section>
</template>

<script>
export default {
  name: "CourseTrain",
  data() {
      return {
        enteredGoalValue: "",
        goals: [],
        // person: {
        //   name: 'Max',
        //   age: 31
        // }
        toggleTaskIsVisible: true,
      };
    },
  computed: {
    buttonCaption() {
      return this.toggleTaskIsVisible ? 'Hide list' : 'Show list'
    }
  },
  methods: {
    toggleTaskList() {
      this.toggleTaskIsVisible = !this.toggleTaskIsVisible
    },
    addGoal() {
      this.goals.push(this.enteredGoalValue)
    },
    removeGoal(index) {
      this.goals.splice(index, 1)
    }
  }
  }

</script>

<style lang="scss">
@import "../../assets/styles/courselist";
</style>