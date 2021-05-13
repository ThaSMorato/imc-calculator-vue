<template>
  <div class="white-bg">
    <div class="row">
      <p class="layer">Tipo :</p>
      <p v-bind:class="`value-${obesity}`">{{ type }}</p>
    </div>
    <div class="row">
      <p class="layer">Grau de Obesidade :</p>
      <p v-bind:class="`value-${obesity}`">{{ obesity }}</p>
    </div>
    <div class="row">
      <p class="layer">Valor :</p>
      <p v-bind:class="`value-${obesity}`">{{ value.toFixed(2) }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: {
    obesity: Number,
    value: Number,
    type: String,
  },
};
</script>

<style scoped>
.white-bg {
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  flex-direction: column;
  border-radius: 10px;
  padding: 20px 0;
}

.white-bg p {
  font-size: 2rem;
  color: #383838;
  font-weight: 400;
  margin: 0 10px;
}

.row {
  display: flex;
  justify-content: flex-start;
  align-self: center;
  flex-direction: row;
  width: 100%;
}

.white-bg .value-0 {
  color: green;
  font-weight: bold;
}

.white-bg .value-1 {
  color: orange;
  font-weight: bold;
}

.white-bg .value-2 {
  color: orangered;
  font-weight: bold;
}

.white-bg .value-3 {
  color: red;
  font-weight: bold;
}
</style>
