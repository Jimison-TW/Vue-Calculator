<template>
    <div id="number_button">
        <div id="buttonContainer">
            <div class="buttonDiv" v-for="(value, key) in numbers" :key="key">
                <input
                    type="button"
                    class="number_button"
                    @click="pressNumber(value)"
                    :value="value"/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'NumberButton',
  props: {
    result: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      numbers: [7, 8, 9, 4, 5, 6, 1, 2, 3, 0],
    };
  },
  methods: {
    pressNumber(value) {
      this.$emit('onNumberClick', value);
    },
  },
};
</script>

<style>
.number_button {
  width: 40px;
  height: 40px;
}
.buttonDiv {
  width: calc(100% / 3);
}
#buttonContainer {
  width: 150px;
  display: flex;
  flex-wrap: wrap;
}
input {
  width: calc(100% / 3);
}
</style>
