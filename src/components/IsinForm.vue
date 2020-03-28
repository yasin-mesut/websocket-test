<template>
  <form
    class="isin-form"
    @submit="submit"
  >
    <label
      for="isin"
      class="isin-form__label"
    >
      Add ISIN here
    </label>
    <input
      id="isin"
      class="isin-form__input"
      v-model="isin"
    >
    <div class="isin-form__hints">
      Hit enter to submit your input
    </div>
  </form>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class IsinForm extends Vue {
  isin = 'DE000BASF111';

  submit($event: Event) {
    $event.preventDefault();

    this.$emit('addIsin', this.isin);
    this.resetIsin();
  }

  resetIsin() {
    this.isin = '';
  }
}
</script>

<style scoped lang="scss">
  $gray: #808080;

  .isin-form {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin: 1rem;

    &__input {
      margin-left: 1rem;
      border: 1px solid $gray;
      border-radius: 3px;
      flex-grow: 1;
    }

    &__hints {
      font-size: 0.85rem;
      color: $gray;
      flex-basis: 100%;
    }
  }
</style>
