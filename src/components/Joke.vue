<template>
  <div class="container-joke">
    <h1 v-if="isLoading">Loading...</h1>
    <div class="joke" v-else-if="oneJoke">
      <div>
        <h1>
          {{ oneJoke }}
        </h1>
        <button @click="copyToClipboard('joke')">Copy</button>
      </div>
    </div>
    <div class="joke" v-else>
      <div>
        <h1 id="setup">
          {{ setup }}
        </h1>
        <button @click="copyToClipboard('setup')">Copy</button>
      </div>
      <div id="delivery">
        <h1>{{ delivery }}</h1>
        <button @click="copyToClipboard('delivery')">Copy</button>
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
    copyToClipboard(method) {
      var textToCopy = "";

      if (method == "joke") {
        textToCopy = this.oneJoke;
      } else if (method == "setup") {
        textToCopy = this.setup;
      } else {
        textToCopy = this.delivery;
      }

      if (navigator.clipboard && window.isSecureContext) {
        return navigator.clipboard.writeText(textToCopy);
      } else {
        let textArea = document.createElement("textarea");
        textArea.value = textToCopy;
        textArea.style.position = "fixed";
        textArea.style.left = "-999999px";
        textArea.style.top = "-999999px";
        document.body.appendChild(textArea);
        textArea.focus();
        textArea.select();
        return new Promise((res, rej) => {
          document.execCommand("copy") ? res() : rej();
          textArea.remove();
          alert("Copied to Clipboard");
        });
      }
    },
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
  width: 3rem;
}

button:hover {
  cursor: pointer;
}

.joke {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
</style>
