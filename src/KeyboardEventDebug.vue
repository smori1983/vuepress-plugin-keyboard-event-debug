<template>
  <div class="debug-block">
    <input
      type="text"
      class="input"
      :value="input"
      @input="input = $event.target.value"
      @keydown="registerKeyDown($event)"
      @keyup="registerKeyUp($event)"
    />
    <button @click="clearOutputHistory">Clear</button>
    <table v-if="hasOutputHistory">
      <tr>
        <th>event</th>
        <th>key</th>
        <th>keyCode</th>
        <th>text</th>
      </tr>
      <tr v-for="item in outputHistory">
        <td v-html="item.phase"></td>
        <td v-html="item.key"></td>
        <td v-html="item.keyCode"></td>
        <td v-html="item.text"></td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: '',
      outputHistory: [],
    };
  },

  computed: {
    hasOutputHistory: function () {
      return this.outputHistory.length > 0;
    }
  },

  methods: {
    registerKeyDown(event) {
      this.outputHistory.unshift({
        phase: 'keydown',
        key: event.key,
        keyCode: event.keyCode,
        text: this.input,
      });
    },

    registerKeyUp(event) {
      this.outputHistory.unshift({
        phase: 'keyup',
        key: event.key,
        keyCode: event.keyCode,
        text: this.input,
      });
    },

    clearOutputHistory() {
      this.input = '';
      this.outputHistory = [];
    },
  },
};
</script>

<style lang="stylus" scoped>
.debug-block {
  input {
    cursor: text;
    width: 30rem;
    height: 2rem;
    line-height: 2rem;
    border: 1px solid darken($borderColor, 10%);
    border-radius: 0.4rem;
    font-size: 0.9rem;
    padding: 0 0.5rem;
  }
  button {
    cursor: pointer;
    height: 2rem;
    line-height: 2rem;
    color: lighten($accentColor, 93%);
    background-color: $accentColor;
    border: 1px solid darken($borderColor, 10%);
    border-radius: 0.4rem;
    font-size: 0.9rem;
    padding: 0 0.5rem;

    &:hover {
      color: $textColor;
      background-color: lighten($accentColor, 93%);
    }
  }
}
</style>
