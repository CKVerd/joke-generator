<template>
  <div class="container">
    <div class="main-container">
      <div class="title-div">
        <h1>Joke Generator</h1>
      </div>
      <div class="selectors-div">
        <div class="category-div selector">
          <h1>Category</h1>
          <div class="main-category-selectors">
            <div>
              <div>
                <input
                  @change="checkIn($event.target.value)"
                  type="checkbox"
                  id="any"
                  value="any"
                  v-model="chosenCategory"
                />
                <label for="any">Any</label>
              </div>
            </div>
            <div class="category-inputs">
              <div class="category-divide">
                <div class="cat">
                  <input
                    @change="checkIn($event.target.value)"
                    type="checkbox"
                    id="programming"
                    value="programming"
                    v-model="chosenCategory"
                  />
                  <label for="programming">Programming</label>
                </div>
                <div class="cat">
                  <input
                    @change="checkIn($event.target.value)"
                    type="checkbox"
                    id="misc"
                    value="misc"
                    v-model="chosenCategory"
                  />
                  <label for="misc">Misc</label>
                </div>
                <div class="cat">
                  <input
                    @change="checkIn($event.target.value)"
                    type="checkbox"
                    id="dark"
                    value="dark"
                    v-model="chosenCategory"
                  />
                  <label for="dark">Dark</label>
                </div>
                <div class="cat">
                  <input
                    @change="checkIn($event.target.value)"
                    type="checkbox"
                    id="pun"
                    value="pun"
                    v-model="chosenCategory"
                  />
                  <label for="pun">Pun</label>
                </div>
              </div>
              <div class="category-divide">
                <div class="cat">
                  <input
                    @change="checkIn($event.target.value)"
                    type="checkbox"
                    id="spooky"
                    value="spooky"
                    v-model="chosenCategory"
                  />
                  <label for="spooky">Spooky</label>
                </div>
                <div class="cat">
                  <input
                    @change="checkIn($event.target.value)"
                    type="checkbox"
                    id="christmas"
                    value="christmas"
                    v-model="chosenCategory"
                  />
                  <label for="christmas">Christmas</label>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="flags-div selector">
          <h1>Flags/Blacklist</h1>
          <div class="main-flags-div">
            <div class="cat">
              <input type="checkbox" id="nsfw" value="nsfw" v-model="flags" />
              <label for="nsfw">NSFW</label>
            </div>
            <div class="cat">
              <input
                type="checkbox"
                id="religious"
                value="religious"
                v-model="flags"
              />
              <label for="religious">Religious</label>
            </div>
            <div class="cat">
              <input
                type="checkbox"
                id="political"
                value="political"
                v-model="flags"
              />
              <label for="political">Political</label>
            </div>
            <div class="cat">
              <input
                type="checkbox"
                id="racist"
                value="racist"
                v-model="flags"
              />
              <label for="racist">Racist</label>
            </div>
            <div class="cat">
              <input
                type="checkbox"
                id="sexist"
                value="sexist"
                v-model="flags"
              />
              <label for="sexist">Sexist</label>
            </div>
            <div class="cat">
              <input
                type="checkbox"
                id="explicit"
                value="explicit"
                v-model="flags"
              />
              <label for="explicit">Explicit</label>
            </div>
          </div>
        </div>
        <div class="jokeType-div selector">
          <h1>Joke Type</h1>
          <div class="main-joke-div">
            <div class="cat">
              <input
                type="checkbox"
                id="single"
                value="single"
                v-model="joketype"
              />
              <label for="single">Single</label>
            </div>
            <div class="cat">
              <input
                type="checkbox"
                id="twopart"
                value="twopart"
                v-model="joketype"
              />
              <label for="twopart">Two Part</label>
            </div>
          </div>
        </div>
      </div>
      <div class="button-div">
        <button @click="queryAPI">Generate Joke</button>
      </div>
      <div class="joke-container">
        <Joke
          v-if="jokes.length"
          :setup="queryData.data?.setup"
          :delivery="queryData.data?.delivery"
          :isLoading="isLoading"
          :oneJoke="queryData.data?.joke"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../components/Joke.vue";

export default {
  components: { Joke },
  name: "Home",
  data() {
    return {
      chosenCategory: ["any"],
      flags: [],
      joketype: ["single", "twopart"],
      isLoading: false,
      queryData: null,
      jokes: [],
    };
  },
  methods: {
    log() {
      console.log(this.joketype);
    },
    checkIn(val) {
      if (val != "any") {
        const index = this.chosenCategory.indexOf("any");
        if (index > -1) {
          this.chosenCategory.splice(index, 1);
        }
      } else {
        this.chosenCategory.length = 0;
        this.chosenCategory.push("any");
      }
    },
    async queryAPI() {
      this.isLoading = true;
      const url = "https://v2.jokeapi.dev/joke/" + this.chosenCategory.toString();
      const parameters = {
        blacklistFlags: this.flags.toString(),
        type: this.joketype.toString(),
      };

      await axios.get(url, { params: parameters }).then((val) => {
        this.queryData = val;
        console.log(this.queryData);
        this.jokes.push("asd");
        this.isLoading = false;
      });
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700&display=swap");

.container {
  display: flex;
  justify-content: center;
  align-content: center;
  width: 100vw;
  height: 100vh;
  background-color: rgb(243, 243, 243);
  font-family: "Roboto", sans-serif;
}

.main-container {
  width: 80%;
  display: flex;
  flex-direction: column;
}

.title-div {
  width: 100%;
  height: 12vh;
  padding-top: 1.5rem;
}

.selectors-div {
  height: 30vh;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.selector {
  /* border: 1px solid black; */
  width: 30%;
  height: 100%;
  border-radius: 10px;
  padding: 1rem;
  box-shadow: 8px 8px 20px rgba(0, 0, 0, 0.15), -8px -8px 10px white;
}

.title-div h1 {
  font-size: 2rem;
}

.selector h1 {
  font-size: 1.25rem;
}

.main-category-selectors {
  display: flex;
  flex-direction: column;
  padding: 1rem;
}

.category-inputs {
  display: flex;
}

.category-divide {
  width: 50%;
  height: 100%;
  padding-top: 1rem;
}

.cat {
  margin-top: 0.5rem;
}
label {
  margin-left: 0.5rem;
}

.main-flags-div {
  padding: 0.3rem;
  padding-left: 1rem;
}

.main-joke-div {
  padding: 0.3rem;
  padding-left: 1rem;
}

.button-div {
  width: 100%;
  height: 10vh;
  padding: 0 1.25rem;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.button-div button {
  height: 50%;
  width: 10rem;
  border-radius: 10px;
  outline: none;
  border: none;
  box-shadow: 8px 8px 20px rgba(0, 0, 0, 0.15), -4px -4px 10px white;
  background-color: white;
  transition: 0.4s;
  font-size: 0.85rem;
}

.button-div button:hover {
  background-color: rgb(83, 96, 173);
  color: white;
  cursor: pointer;
}

.joke-container {
  width: 100%;
  padding: 0 1.25rem;
}
</style>
