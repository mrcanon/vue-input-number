<template>
  <div>
    <input type="number" v-on:blur="handleChange(value)" v-model="value"/>
    <div class="input-number-controls" v-if="controls">
      <button class="control" v-on:click="handleChange(value + 1)">+</button>
      <button class="control" v-on:click="handleChange(value - 1)">-</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'input-number',
  props: {
    min: {
      type: Number
    },
    max: {
      type: Number,
      required: false
    },
    change: {
      type: Function
    },
    controls: {
      type: Boolean,
      default: true
    },
  },

  data () {
    return {
      value: 0
    }
  },

  methods: {
    handleChange (value) {
      const toInt = parseInt(value)
      const { min, max } = this
      if (!Number.isFinite(toInt)) {
        this.value = min
      } else if (toInt < min) {
        this.value = min
      } else if (toInt > max) {
        this.value = max
      } else {
        this.value = toInt
      }
      this.change(toInt)
    }
  }
}
</script>

<style scoped>
  .input-number-controls {
    display: inline-block;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
</style>
