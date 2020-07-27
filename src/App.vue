<template>
  <div id="app" class="bg-dark text-white text-center container-fluid">
    <div class="row justify-content-center">
      <div class="col-12">
        <img alt="Vue logo" src="./assets/logo.png" />
      </div>
      <div class="col-6 col-md-4" id="target">
        <h1>{{target.name}}</h1>
        <h1
          class="text-success"
          :class="{'text-warning': target.health <= 75, 'text-danger': target.health <= 50}"
          v-if="target.health > 0"
        >{{target.health < 0 ? 0 : target.health}}</h1>
        <h1 v-else>Its dead jim.</h1>
        <p :class="statusColor()">hits: {{target.hits}}</p>
        <button
          type="button"
          class="btn btn-danger mx-2"
          @click="attackTarget(attack.damage)"
          v-for="(attack, attackIndex) in attacks"
          :key="attack.name"
        >{{attack.name}}</button>
        <button class="btn btn-primary m-2 btn-block" @click="reset()">Reset</button>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "App",
  data() {
    return {
      target: {
        name: "Bob",
        health: 100,
        hits: 0,
      },
      attacks: [
        {
          name: "Slap",
          damage: 1,
        },
        {
          name: "Punch",
          damage: 5,
        },
        {
          name: "Kick",
          damage: 10,
        },
      ],
    };
  },
  methods: {
    attackTarget(dmg) {
      this.target.health -= dmg;
      this.target.hits++;
    },
    statusColor() {
      let className = "text-success";
      if (this.target.health <= 50) {
        className = "text-danger";
      } else if (this.target.health <= 75) {
        className = "text-warning";
      }
      return className;
    },
    reset() {
      this.target.health = 100;
      this.target.hits = 0;
    },
  },
};
</script>
