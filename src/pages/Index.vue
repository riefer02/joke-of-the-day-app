<template>
  <q-page class="flex flex-center">
    <q-card dark bordered class="bg-grey-9 my-card">
      <q-card-section>
        <div class="flex justify-between">
          <div class="text-h6">Joke of the Day</div>
          <q-btn size="sm" class="bg-white text-grey-9" @click="getJoke()"
            >New Joke</q-btn
          >
        </div>
        <div class="text-subtitle2">by Jordan Hughes</div>
      </q-card-section>

      <q-separator dark inset />

      <q-card-section>
        {{ setup ? setup : joke }}
      </q-card-section>
      <div v-if="!joke">
        <div class="flex flex-center">
          <q-btn class="q-mb-md bg-white text-grey-9" @click="revealDelivery()"
            >Punchline!</q-btn
          >
        </div>

        <q-card-section v-if="revealJoke">
          {{ delivery }}
        </q-card-section>
      </div>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data: () => ({
    delivery: undefined,
    setup: undefined,
    joke: undefined,
    revealJoke: false,
  }),
  mounted() {
    this.getJoke();
  },
  methods: {
    getJoke() {
      this.$axios
        .get("https://v2.jokeapi.dev/joke/Any?blacklistFlags=racist,sexist")
        .then((res) => {
          console.log(res);
          this.setup = res.data.setup;
          this.delivery = res.data.delivery;
          this.joke = res.data.joke;
        });
    },
    revealDelivery() {
      this.revealJoke = true;
    },
  },
};
</script>
