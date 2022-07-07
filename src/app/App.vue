<template>
  <HelloWorld/>
  <CourseList/>
  <CourseGame/>
</template>

<script>

// import HelloWorld from '../components/sections/Hello'
// import CourseList from '../components/sections/CourseList'
import CourseGame from '../components/sections/CourseGame'


export default {
  name: 'App',
  components: {
    // HelloWorld,
    // CourseList,
    CourseGame,
  },
}
</script>

<style lang="scss">
@import "../assets/styles/styles.scss";
</style>

