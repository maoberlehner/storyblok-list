<template>
  <div class="List">
    <ol class="List__list uk-margin-bottom-remove">
      <li
        v-for="(item, index) in model.items"
        :key="index"
        class="List__list-item uk-flex uk-flex-middle"
      >
        <input
          v-model="model.items[index]"
          :aria-label="`List item ${index}`"
          class="uk-form-small uk-width-1-1"
        >
        <a
          class="assets__item-trash"
          aria-label="Remove item"
          @click="removeItem(index)"
        >
          <i class="uk-icon-minus-circle"/>
        </a>
      </li>
    </ol>
    <a
      v-if="!limitReached"
      class="blok__full-btn uk-margin-small-top"
      @click="addItem"
    >
      <i class="uk-icon-plus-circle uk-margin-small-right"/>
      Add item
    </a>
  </div>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  computed: {
    limitReached() {
      return this.options.limit && this.model.items.length >= this.options.limit;
    },
  },
  watch: {
    model: {
      deep: true,
      handler(value) {
        this.$emit(`changed-model`, value);
      },
    },
  },
  methods: {
    addItem() {
      this.model.items.push(``);
    },
    removeItem(index) {
      this.model.items = this.model.items.filter((_, i) => i !== index);
    },
    initWith() {
      return {
        items: [``],
        plugin: `list`,
      };
    },
  },
};
</script>

<style>
.List__list {
  padding-left: 0;
}

.List__list-item + .List__list-item {
  margin-top: 5px;
}
</style>
