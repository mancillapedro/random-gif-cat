<template>
  <form @submit.prevent="valuesForm">
    <fieldset :disabled="disabled">
      <ul>
        <li>
          <label for="title">Titulo: </label>
          <div>
            <input
              id="title"
              name="title"
              v-model="title"
              type="text"
              minlength="1"
              required
            />
          </div>
        </li>
        <li>
          <label for="filter">Filtro: </label>
          <div>
            <select id="filter" name="filter" v-model="filter" required>
              <option value="" disabled>Selecciona un filtro...</option>
              <option
                v-for="(filter, i) in selects.filters"
                :key="i"
                v-text="filter"
                :value="filter"
              />
            </select>
          </div>
        </li>
        <li>
          <label for="color">Color: </label>
          <div>
            <select id="color" name="color" v-model="color" required>
              <option value="" disabled>Selecciona un color...</option>
              <option
                v-for="(value, key) in selects.colors"
                :key="value"
                v-text="key"
                :value="value"
              />
            </select>
            <div class="rounded" :style="styleObj"></div>
          </div>
        </li>
        <li>
          <label for="size">Tamaño: </label>
          <div>
            <input
              id="size"
              name="size"
              v-model="size"
              type="number"
              min="1"
              required
            />
          </div>
        </li>
      </ul>
      <button type="submit">Obtener mi gatito</button>
    </fieldset>
  </form>
</template>

<script>
export default {
  name: "FormSearch",
  props: {
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  data: function () {
    return {
      title: "",
      filter: "",
      color: "",
      size: null,
      selects: {
        filters: [
          "blur",
          "mono",
          "sepia",
          "negative",
          "paint",
          // "pixel", // opción pixel no disponible para gif
        ],
        colors: {
          rojo: "red",
          azul: "blue",
          verde: "green",
          blanco: "white",
          amarillo: "yellow",
        },
      },
      styleObj: {
        "background-color": "gray",
      },
    };
  },
  computed: {
    parseInputs() {
      return `${this.title}?filter=${this.filter}&color=${this.color}&size=${this.size}`;
    },
  },
  methods: {
    valuesForm() {
      this.$emit("valuesForm", { path: this.parseInputs });
    },
    cleanValues() {
      this.title = "";
      this.filter = "";
      this.color = "";
      this.size = null;
    },
  },
  watch: {
    color(newColor) {
      this.styleObj["background-color"] = newColor || "gray";
    },
    disabled(newDisabled){
      newDisabled || this.cleanValues()
    }
  },
};
</script>

<style scoped>
.rounded {
  display: inline-block;
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  vertical-align: middle;
  margin-left: 1rem;
}
fieldset {
  border: none;
}
ul {
  padding: 1rem 0;
  text-align: left;
  background-color: #f08080;
}
li {
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-content: center;
  gap: 2rem;
  padding: 0.5rem 0;
}
li > label {
  text-align: right;
}
button {
  margin: 1rem auto;
  padding: 0.25rem 0.75rem;
  cursor: pointer;
}
</style>