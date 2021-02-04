<template>
  <div class="games-list">
    <GenresSlider />
    <div class="container mt-5 mb-5">
      <div class="row">
        <div class="col">
          <div class="loader-wrapper" v-if="isLoading">
            <PulseLoader :loading="true" :color="color" />
          </div>
          <div v-else>
            <FeaturedGame
              :featuredGame="featuredGame"
              @new-game-selected="gameSelectedHandler"
            />
            <GamesCard
              :games="recommendedGames"
              @new-game-selected="gameSelectedHandler"
            />
            <GamesCard
              :games="popularGames"
              @new-game-selected="gameSelectedHandler"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import GenresSlider from "../components/GenresSlider";
import FeaturedGame from "../components/FeaturedGame";
import GamesCard from "../components/GamesCard";

export default {
  head() {
    return {
      title: "Games Platform",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Some description for Games Page"
        }
      ]
    };
  },

  components: {
    PulseLoader,
    GenresSlider,
    FeaturedGame,
    GamesCard
  },
  computed: {
    ...mapGetters({
      isLoading: "games/getLoadingState",
      featuredGame: "games/getFeaturedGame",
      recommendedGames: "games/getRecommendedGames",
      popularGames: "games/getPopularGames"
    })
  },
  methods: {
    ...mapActions({
      selectGame: "games/selectGame",
      fetchGames: "games/fetchGames"
    }),

    gameSelectedHandler(game) {
      this.selectGame(game);
      this.$router.push("/details");
    }
  },
  created() {
    this.fetchGames();
  },
  data() {
    return {
      color: "#5bc0de"
    };
  }
};
</script>

<style scoped>
.loader-wrapper {
  width: 100%;
  height: 56vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
