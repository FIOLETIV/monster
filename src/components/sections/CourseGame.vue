<template>
  <header>
    <h1>Monster Slayer</h1>
  </header>
    <section id="monster" class="container">
      <h2>Monster Health</h2>
      <div class="healthbar">
        <div class="healthbar__value" :style="monsterBarStyles"></div>
      </div>
    </section>
    <section id="player" class="container">
      <h2>Your Health</h2>
      <div class="healthbar">
        <div class="healthbar__value" :style="playerBarStyles"></div>
      </div>
    </section>
    <section class="container" v-if="winner">
      <h2>Game over!</h2>
      <h3 v-if="winner === 'Monster'">You Lost!</h3>
      <h3 v-else-if="winner === 'Player'">You Won!</h3>
      <h3 v-else>It's a draw!</h3>
      <button @click="startGame">Start New Game</button>
    </section>
    <section id="controls" v-else>
      <button @click="attackMonster">ATTACK</button>
      <button :disabled="mayUseSpecialAttack" @click="specialAttackMonster">SPECIAL ATTACK</button>
      <button @click="healPlayer">HEAL</button>
      <button @click="surrender">SURRENDER</button>
    </section>
    <section id="log" class="container">
      <h2>Battle Log</h2>
      <ul>
        <li v-for="(logMessage, index) in logMessages" :key="index">
          <span
              :class="{'log--player': logMessage.actionBy === 'Player', 'log--monster': logMessage.actionBy === 'Monster'}"
          >{{ logMessage.actionBy === 'Player' ? 'Player' : 'Monster'
            }}</span
          >
          <span v-if="logMessage.actionType === 'heal'">
              heals himself for
              <span class="log--heal">{{ logMessage.actionValue }}</span></span
          >
          <span v-else>
              attacks and deals
              <span class="log--damage">{{ logMessage.actionValue }}</span>
            </span>
        </li>
      </ul>
    </section>
</template>

<script>
export default {
  name: "CourseGame",
  data() {
    return {
      playerHealth: 100,
      monsterHealth: 100,
      currentRound: 0,
      winner: null,
      logMessages: [],
    }
  },
  computed: {
    monsterBarStyles() {
      if (this.monsterHealth < 0) {
        return { width: '0%'}
      }
      return {width: this.monsterHealth + '%'};
    },
    playerBarStyles() {
      if (this.playerHealth < 0) {
        return { width: '0%' }
      }
      return {width: this.playerHealth + '%'};
    },
    mayUseSpecialAttack() {
      return this.currentRound % 3 !== 0
    },
  },
  watch: {
    playerHealth(value) {
      if(value <= 0 && this.monsterHealth <= 0){
        this.winner = 'Draw'
      } else if (value <= 0) {
        this.winner = 'Monster'
      }
    },
    monsterHealth(value) {
      if(value <= 0 && this.playerHealth <= 0){
        this.winner = 'Draw'
      } else if(value <= 0){
        this.winner = 'Player'
      }
    }
  },
  methods: {
    startGame () {
      this.playerHealth = 100;
      this.monsterHealth = 100;
      this.winner = null;
      this.currentRound = 0;
      this.logMessages = [];
    },
    attackMonster() {
      this.currentRound++
      const attackValue = getRandomValue (5, 12)
      this.monsterHealth -= attackValue;
      this.addLogMessage('Player', 'Attack', attackValue)
      this.attackPlayer();
    },
    attackPlayer() {
      const attackValue = getRandomValue(8, 15)
      this.playerHealth -= attackValue;
      this.addLogMessage('Monster', 'Attack', attackValue)
    },
    specialAttackMonster() {
      this.currentRound++
      const attackValue = getRandomValue(10, 25)
      this.monsterHealth -= attackValue;
      this.addLogMessage('Player', 'Special Attack', attackValue)
      this.attackPlayer();
    },
    healPlayer() {
      this.currentRound++
      const healValue = getRandomValue(8, 20)
      if (this.playerHealth + healValue > 100) {
        this.playerHealth = 100
      } else {
        this.playerHealth += healValue;
      }
      this.addLogMessage('Player', 'heal', healValue)
      this.attackPlayer();
    },
    surrender() {
      this.winner = 'Monster'
    },
    addLogMessage(who, what, value) {
      this.logMessages.unshift({
        actionBy: who,
        actionType: what,
        actionValue: value
      })
    },
  }
}

function getRandomValue(min, max) {
  return Math.floor(Math.random() * (max-min)) + min;
}
</script>

<style lang="scss" scoped src="../../assets/styles/coursegame.scss">

</style>