<template>
  <q-page class="flex flex-center">
    <q-card dark bordered class="bg-grey-9 my-card">
      <q-card-section>
        <div class="text-h6">Joke of the Day</div>
        <div class="text-subtitle2">by Jordan Hughes</div>
      </q-card-section>

      <q-separator dark inset />

      <q-card-section>
        {{ setup }}
      </q-card-section>
      <div class="flex flex-center">
        <q-btn class="q-mb-md" @click="revealDelivery()">Punchline!</q-btn>
      </div>
      <q-card-section v-if="revealJoke">
        {{ delivery }}
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data: () => ({
    delivery: undefined,
    setup: undefined,
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
        });
    },
    revealDelivery() {
      this.revealJoke = true;
    },
  },
};
</script>
