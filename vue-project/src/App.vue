<script>

import { ref } from "vue"
import HeaderGame from "./components/HeaderGame.vue";
import Player from "./components/Player.vue";
import ButtonControl from "./components/ButtonControl.vue";
import LogBattle from "./components/logBattle.vue";

export default {

  // define child compontens
  components: { HeaderGame, Player, ButtonControl, LogBattle },

  setup() {

    const round = ref("0");

    return {
      round
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

    <!-- section enemy -->
    <Player title="Enemy"></Player>

    <!-- section player -->
    <Player title="You"></Player>

    <!-- section controls -->
    <section class="container-fluid mt-5 d-flex flex-column gap-4">

      <!-- row buttons attack -->
      <div class="row justify-content-center gap-4 gap-sm-0">

        <!-- button attack -->
        <div class="col-12 col-sm-6 col-md-3 text-center">
          <ButtonControl title="Attack" color="primary" />
        </div>

        <!-- button attack special -->
        <div class="col-12 col-sm-6 col-md-3 text-center">
          <ButtonControl title="Special Attack" color="primary" />
        </div>

      </div>

      <!-- row buttons medikit/gamer over -->
      <div class="row justify-content-center gap-4 gap-sm-0">

        <!-- button meidkit -->
        <div class="col-12 col-sm-6 col-md-3 text-center">
          <ButtonControl title="Medikit" color="success" />
        </div>

        <!-- button gamer over -->
        <div class="col-12 col-sm-6 col-md-3 text-center">
          <ButtonControl title="Gamer Over!" color="danger" />
        </div>

      </div>

    </section>

    <!-- section log -->
    <LogBattle title="Battle log" />

  </main>

</template>

<style scoped></style>
