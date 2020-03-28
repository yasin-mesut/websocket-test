<template>
  <div id="app">
    <div class="form-wrapper">
      <IsinForm @addIsin="addIsinToList" />
    </div>
    <div class="isin-list">
      <IsinItem
        :key="isin.isin"
        v-for="isin in isinList"
        :isin="isin"
        @removeIsin="removeIsinFromList"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import IsinForm from '@/components/IsinForm.vue';
import IsinItem from '@/components/IsinItem.vue';

@Component({
  components: {
    IsinForm,
    IsinItem,
  },
})
export default class App extends Vue {
  ws!: WebSocket;

  wsUrl = 'ws://159.89.15.214:8080/';

  isinList: { } = { };

  created() {
    this.ws = new WebSocket(this.wsUrl);

    this.ws.onmessage = (event) => {
      const json = JSON.parse(event.data);

      this.$set(this.isinList, json.isin, json);
    };
  }

  addIsinToList(isin: string) {
    const jsonString = JSON.stringify({
      subscribe: isin,
    });

    this.ws.send(jsonString);
  }

  removeIsinFromList(isin: string) {
    const jsonString = JSON.stringify({
      unsubscribe: isin,
    });

    this.$delete(this.isinList, isin);
    this.ws.send(jsonString);
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
