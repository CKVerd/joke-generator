<template>
  <div class="container-joke">
    <h1 v-if="isLoading">Loading...</h1>
    <div class="joke" v-else-if="oneJoke">
      <div>
        <h1>
          {{ oneJoke }}
        </h1>
        <button @click="copyText('joke')">Copy</button>
      </div>
    </div>
    <div class="joke" v-else>
      <div>
        <h1>
          {{ setup }}
        </h1>
        <button @click="copyText('setup')">Copy</button>
      </div>
      <div>
        <h1>{{ delivery }}</h1>
        <button @click="copyText('delivery')">Copy</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Joke",
  data() {
    return {};
  },
  methods: {
      copyText(method) {
          if (method == "joke") {
              navigator.clipboard.writeText(this.oneJoke);
          } else if (method == "setup") {
              navigator.clipboard.writeText(this.setup);
          } else {
              navigator.clipboard.writeText(this.delivery)
          }
      }
  },
  props: {
    isLoading: Boolean,
    setup: String,
    delivery: String,
    oneJoke: String,
  },
};
</script>

<style scoped>
.container-joke {
  width: 100%;
  height: 15rem;
  box-shadow: 8px 8px 20px rgba(0, 0, 0, 0.15), -8px -8px 10px white;
  padding: 2rem;
  display: flex;
  flex-direction: column;
}

.container-joke h1 {
  font-size: 1.5rem;
  margin-top: 0.75rem;
  width: 80%;
}

.container-joke div {
  display: flex;
}

.container-joke button {
  margin-left: auto;
  margin-top: 0.75rem;
  height: 2rem;
}

.joke {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
</style>
