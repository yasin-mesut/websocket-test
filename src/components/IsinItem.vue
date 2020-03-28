<template>
  <div class="isin-item">
    <div class="isin-item__name">
      {{ isin.isin }}
      <span
        class="isin-item__remove"
        @click="removeIsin"
      >
        X
      </span>
    </div>
    <div class="isin-item__price">
      Price:
      {{ getNum(isin.price) }}
    </div>
    <div class="isin-item__bid">
      Bid:
      {{ getNum(isin.bid) }}
    </div>
    <div class="isin-item__ask">
      Ask:
      {{ getNum(isin.ask) }}
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class IsinItem extends Vue {
  @Prop() isin!: {
    isin: string;
    price: number;
    bid: number;
    ask: number;
  };

  getNum(num: number) {
    return parseFloat(num.toFixed(2));
  }

  removeIsin() {
    this.$emit('removeIsin', this.isin.isin);
  }
}
</script>

<style scoped lang="scss">
  .isin-item {
    display: flex;
    padding: 1rem 0;
    margin-top: -1px;
    border: 1px solid;
    flex-direction: row;
    flex-wrap: wrap;

    &__name {
      position: relative;
      flex-basis: 100%;
      border-bottom: 1px solid;
      padding-bottom: 0.5rem;
      margin-bottom: 0.5rem;
    }

    &__remove {
      position: absolute;
      top: -0.5rem;
      right: 0.5rem;
      padding: 0 0.25rem;
      color: #fff;
      background-color: #ff0000;
      border-radius: 50%;
      cursor: pointer;
    }

    &__price,
    &__bid,
    &__ask {
      flex-grow: 1;
    }
  }
</style>
