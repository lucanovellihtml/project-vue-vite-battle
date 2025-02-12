<script>

import { ref, computed, watch } from "vue"
import HeaderGame from "./components/HeaderGame.vue";
import Player from "./components/Player.vue";
import ButtonControl from "./components/ButtonControl.vue";
import LogBattle from "./components/LogBattle.vue";
import MessageEndGame from "./components/MessageEndGame.vue";

//function random
const getRandomValue = (min, max) => {
  return Math.floor(Math.random() * (max - min) + min);
}


export default {

  // define child compontens
  components: { HeaderGame, Player, ButtonControl, LogBattle, MessageEndGame },

  setup() {

    //array log
    const logMessages = ref([]);

    //variable message end game
    const message = ref();

    //variable count round
    const round = ref("0");

    //variable health enemy total
    const healthEnemyTotal = ref(100);

    //variable health player total
    const healthPlayerTotal = ref(100);

    //variableplayer now
    const healthNow = ref(100);

    //variable attack enemy
    const attackEnemy = ref();

    //variable attack player
    const attackPlayer = ref();

    //variable medikit
    const medikit = 20;

    //function attack player
    const handleClickAttack = () => {
      //console.log("Hai cliccato attack");
      attackPlayer.value = getRandomValue(1, 20);

      if (healthEnemyTotal.value - attackPlayer.value <= 0)
        healthEnemyTotal.value = 0;
      else
        healthEnemyTotal.value -= attackPlayer.value;

      //console.log("Attacco player ->", attackPlayer.value);
      recordLog("player", "attack", attackPlayer.value);

      actionAttackEnemy();
      round.value++;
    }

    //function super attack player
    const handleClickSuperAttack = () => {
      //console.log("Hai cliccato super attack");
      attackPlayer.value = getRandomValue(10, 40);

      if (healthEnemyTotal.value - attackPlayer.value <= 0)
        healthEnemyTotal.value = 0;
      else
        healthEnemyTotal.value -= attackPlayer.value;

      //console.log("Super attacco player ->", attackPlayer);
      recordLog("player", "super attack", attackPlayer.value);

      actionAttackEnemy();
      round.value++;
    }

    //function medikit player
    const handleClickMedikit = () => {
      //console.log("Hai cliccato medikit");
      if (healthPlayerTotal.value + medikit > 100)
        healthPlayerTotal.value = 100;
      else
        healthPlayerTotal.value += medikit;

      round.value++;
      //console.log("Vita medicata -> ", healthPlayerTotal.value);
      recordLog("player", "medikit", medikit);

      actionAttackEnemy();
    }

    //function gamer over player
    const handleClickGameOver = () => {
      //console.log("Hai cliccato game over");
      healthPlayerTotal.value = 0;
      healthNow.value = "width:" + healthPlayerTotal.value + "%";
      message.value = "Gamer over";

      recordLog("player", "gamer over", healthPlayerTotal.value);
    }

    //function attack enemy
    const actionAttackEnemy = () => {
      //console.log("Il nemico ha attaccato");
      attackEnemy.value = getRandomValue(1, 40);

      if (healthPlayerTotal.value - attackEnemy.value <= 0)
        healthPlayerTotal.value = 0;
      else
        healthPlayerTotal.value -= attackEnemy.value;

      //console.log("Attacco nemico ->", attackEnemy.value);

      recordLog("enemy", "attack", attackEnemy.value);
    }

    //computed to disable or active button super attack
    const attackEnemyDisabled = computed(() => {
      if (round.value < 3)
        return true
      else
        return false
    })

    //computed to disable or active button medikit
    const actionMedikitDisabled = computed(() => {
      if (round.value < 3 || healthPlayerTotal.value >= 50)
        return true
      else
        return false
    })

    //watch to check if winner is enemy
    watch(healthEnemyTotal, (healthEnemyTotal, prevHealthEnemyTotal) => {

      if (healthEnemyTotal.value <= 0 && healthPlayerTotal.value <= 0) {
        message.value = "Tie";
      }
      else if (healthPlayerTotal.value <= 0) {
        message.value = "Game Over";
      }

    })

    //watch to check if winner is player
    watch(healthPlayerTotal, (healthPlayerTotal, prevHealthPlayerTotal) => {

      if (healthPlayerTotal.value <= 0 && healthEnemyTotal.value <= 0) {
        message.value = "Tie";
      }
      else if (healthEnemyTotal.value <= 0) {
        message.value = "Winner";
      }

    })

    //function log
    const recordLog = (who, what, value) => {
      logMessages.value.unshift({
        actionBy: who,
        actionType: what,
        actionValue: value
      })
    }

    //function refresh page
    function refreshPage() {
      window.location.reload();
    }

    return {
      round,
      healthEnemyTotal,
      healthPlayerTotal,
      handleClickAttack,
      handleClickSuperAttack,
      handleClickMedikit,
      handleClickGameOver,
      actionMedikitDisabled,
      attackEnemyDisabled,
      refreshPage,
      message,
      recordLog,
      logMessages
    }

  }

}

</script>

<template>

  <!-- header -->
  <header>

    <!-- header component -->
    <HeaderGame :round="round"></HeaderGame>

  </header>

  <!-- main -->
  <main>

    <!-- section messagge end game -->
    <MessageEndGame v-if="message" :message="message" @click-reset="refreshPage" />

    <!-- section enemy -->
    <Player title="Enemy" :healt="healthEnemyTotal" />

    <!-- section player -->
    <Player title="You" :healt="healthPlayerTotal" />

    <!-- section controls -->
    <template v-if="!message">
      <section class="container-fluid mt-5 d-flex flex-column gap-4">

        <!-- row buttons attack -->
        <div class="row justify-content-center gap-4 gap-sm-0">

          <!-- button attack -->
          <div class="col-12 col-sm-6 col-md-3 text-center">
            <ButtonControl @click="handleClickAttack" title="Attack" color="primary" />
          </div>

          <!-- button attack special -->
          <div class="col-12 col-sm-6 col-md-3 text-center">
            <ButtonControl @click="handleClickSuperAttack" title="Special Attack" color="primary"
              :disabled="attackEnemyDisabled" />
          </div>

        </div>

        <!-- row buttons medikit/gamer over -->
        <div class="row justify-content-center gap-4 gap-sm-0">

          <!-- button meidkit -->
          <div class="col-12 col-sm-6 col-md-3 text-center">
            <ButtonControl @click="handleClickMedikit" title="Medikit" color="success"
              :disabled="actionMedikitDisabled" />
          </div>

          <!-- button gamer over -->
          <div class="col-12 col-sm-6 col-md-3 text-center">
            <ButtonControl @click="handleClickGameOver" title="Gamer Over!" color="danger" />
          </div>

        </div>

      </section>
    </template>

    <!-- section log -->
    <LogBattle title="Battle log" :logs="logMessages" />

  </main>

</template>

<style scoped></style>
