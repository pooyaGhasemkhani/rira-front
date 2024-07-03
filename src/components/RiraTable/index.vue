<template>
  <div class="rira-Table" component="riraTable">
    <table class="table">
      <tr class="tr">
        <td class="td">
          <button @click="removeTodo">Remove</button>
        </td>
        <td class="td">
          {{ content }}
          <input @input="doneTodo" :checked="done" type="checkbox" />
        </td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  name: "RiraTable",

  methods: {
    removeTodo() {
      this.$emit("remove", this.id);
    },
    doneTodo() {
      this.$emit("done", {
        index: this.id,
        done: !this.done,
      });
    },
  },

  props: {
    done: {
      require: true,
      type: String,
    },
    content: {
      require: true,
      type: String,
    },
    id: {
      require: true,
      type: Number,
    },
  },
};
</script>
<style lang="scss">
@import "./styles/index.scss";
</style>
