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
    <button class="clear" @click="clearHistory">Clear</button>
    <table v-if="hasHistory">
      <tr>
        <th>event</th>
        <th>key</th>
        <th>keyCode</th>
        <th>text</th>
      </tr>
      <tr v-for="item in history" :class="item.event">
        <td>{{ item.event }}</td>
        <td>{{ item.key }}</td>
        <td>{{ item.keyCode }}</td>
        <td>{{ item.text }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: '',
      history: [],
    };
  },

  computed: {
    hasHistory: function () {
      return this.history.length > 0;
    }
  },

  methods: {
    registerKeyDown(event) {
      this.history.unshift({
        event: 'keydown',
        key: event.key,
        keyCode: event.keyCode,
        text: this.input,
      });
    },

    registerKeyUp(event) {
      this.history.unshift({
        event: 'keyup',
        key: event.key,
        keyCode: event.keyCode,
        text: this.input,
      });
    },

    clearHistory() {
      this.input = '';
      this.history = [];
    },
  },
};
</script>

<style lang="stylus" scoped>
.debug-block {
  .input {
    cursor: text;
    width: 30rem;
    height: 2rem;
    line-height: 2rem;
    border: 1px solid darken($borderColor, 10%);
    border-radius: 0.4rem;
    font-size: 0.9rem;
    padding: 0 0.5rem;
  }
  .clear {
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
  table {
    tr.keydown {
      background-color: #dddddd;
    }
    tr.keyup {
      background-color: #eeeeee;
    }
  }
}
</style>
