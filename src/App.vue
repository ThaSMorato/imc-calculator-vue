<template>
  <main id="app--imc">
    <div class="container">
      <figure>
        <img src="./assets/logo.png" class="App-logo" alt="vue logo" />
      </figure>
      <h1>IMC</h1>
      <h2>Vue</h2>
      <div class="wrapper">
        <div class="input__group">
          <input type="number" min="0" step="1" v-model="kilos" />
          <label>Kilos</label>
        </div>
        <div class="input__group">
          <input type="number" min="0" step="0.01" v-model="metros" />
          <label>Metros</label>
        </div>
        <div class="result">
          <Result
            v-if="type.isCalculated"
            :obesity="type.obesity"
            :type="type.type"
            :value="type.value"
          />

          <p v-else class="waiting">Aguardando preenchimento de dados</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Result,
  },
  data() {
    return {
      kilos: 0,
      metros: 0,
      imcTypes: [
        {
          min: 0,
          max: 18.59999999999999,
          type: "MAGREZA",
          obesity: 0,
        },
        {
          min: 18.6,
          max: 24.999999999999999,
          type: "NORMAL",
          obesity: 0,
        },
        {
          min: 25,
          max: 29.999999999999999,
          type: "SOBREPESO",
          obesity: 1,
        },
        {
          min: 30,
          max: 39.999999999999999,
          type: "OBESIDADE",
          obesity: 2,
        },
        {
          min: 40,
          max: 9999999,
          type: "OBESIDADE GRAVE",
          obesity: 3,
        },
      ],
      type: { type: "", obesity: 0, value: 0, isCalculated: false },
    };
  },
  watch: {
    kilos: function() {
      this.changeHandler();
    },
    metros: function() {
      this.changeHandler();
    },
  },
  methods: {
    calculateIMC: function() {
      console.log(this.kilos, this.metros);
      const { kilos, metros } = this;
      const imcValue = kilos / (metros * metros);
      console.log(imcValue);
      const result = this.imcTypes.find((imcType) => {
        return imcValue >= imcType.min && imcValue <= imcType.max;
      });
      this.type = {
        isCalculated: true,
        type: result.type,
        obesity: result.obesity,
        value: imcValue,
      };
    },
    changeHandler: function() {
      if (this.checkNull()) {
        this.calculateIMC();
      }
    },
    checkNull: function() {
      return (
        this.kilos > 0 && this.kilos !== undefined && this.metros > 0 && this.metros !== undefined
      );
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

html {
  font-size: 10px;
}
.App-logo {
  height: 4rem;
  pointer-events: none;
}

#app--imc {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container {
  width: 100%;
  max-width: 600px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

h1 {
  color: rgb(196, 196, 4);
  font-size: 12rem;
  font-weight: bold;
}

h2 {
  color: rgb(61, 241, 55);
  font-size: 9rem;
  font-weight: bold;
}

.wrapper {
  width: 100%;
  height: 100%;
  border-radius: 15px;
  border: 1px solid greenyellow;
  background: rgba(224, 213, 213, 0.719);
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.input__group {
  display: flex;
  width: 100%;
  border: 1px solid gray;
  background: gray;
  margin-bottom: 10px;
  border-radius: 7px;
  align-items: center;
}

.input__group input {
  width: 100%;
  height: 2.5rem;
  font-size: 2rem;
  padding: 0.5rem 2.5rem;
  color: rgb(43, 43, 43);
  font-weight: bold;
  text-align: right;
  border-radius: 7px;
  border: 1px solid gray;
}

.input__group label {
  width: 8rem;
  font-size: 2rem;
  font-weight: bold;
  color: rgb(255, 255, 255);
  margin-left: 5px;
}

.result {
  width: 80%;
  padding: 20px;
  border-radius: 10px;
  background-color: wheat;
  border: 1px solid white;
}

.waiting {
  font-size: 2rem;
  color: #707070;
  font-weight: bold;
}
</style>
