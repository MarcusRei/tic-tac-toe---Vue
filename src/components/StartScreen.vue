<script setup lang="ts">
import { ref } from "vue";
import { Player } from "../models/Player";
import { getFromLS } from "../functions";

interface IStartScreenProps {
  gameStarted: boolean;
}

defineProps<IStartScreenProps>();

const emit = defineEmits(["startGame"]);

let players: Player[] = getFromLS("players") || [];

let playerX = "";
let playerO = "";

function addPlayers() {
  if (players.length === 0) {
    players.push(new Player(playerX, 0, "X"), new Player(playerO, 0, "O"));
  }

  emit("startGame", players);
}
</script>

<template>
  <section :class="{ hidden: gameStarted }">
    <h1>StartScreen</h1>
    <form class="player-input" @submit.prevent="addPlayers">
      <div class="inputs">
        <label for="Player X">Player X</label>
        <input v-model="playerX" name="Player X" type="text" />
        <label for="Player O">Player O</label>
        <input v-model="playerO" name="Player O" type="text" />
      </div>
      <button>Start game!</button>
    </form>
  </section>
</template>

<style scoped>
.player-input {
  display: flex;
  flex-direction: column;
  gap: 1em;
  align-items: center;
  border: 1px solid green;
  padding: 1em;
}

.inputs {
  display: flex;
  flex-direction: column;
}

.hidden {
  display: none;
}
</style>
