<template>
  <div class="game-details" v-if="getSelectedGame">
    <div class="container mt-5 mb-5">
      <div class="row">
        <div class="col">
          <!-- IMAGE -->
          <div class="mb-5 shadow-sm">
            <img
              class="img"
              alt="game-image"
              :src="getSelectedGame.background_image"
            />
          </div>
          <!-- MORE_DETAILS_CARD -->
          <MoreDetailsCard v-if="getSelectedGame" :game="getSelectedGame" />
          <!-- Recommended Games -->
          <GamesCard
            :games="getRecommendedGames"
            :withMoreInfo="true"
            @new-game-selected="gameSelectedHandler"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
import GamesCard from "../components/GamesCard";
import MoreDetailsCard from "../components/MoreDetailsCard";

export default {
  components: {
    GamesCard,
    MoreDetailsCard,
  },
  computed: {
    ...mapGetters({
      getSelectedGame: "games/getSelectedGame",
      getRecommendedGames: "games/getRecommendedGames",
    }),
  },
  methods: {
    ...mapActions({
      selectGame: "games/selectGame",
    }),
    gameSelectedHandler(game) {
      this.selectGame(game);
    },
  },
  created() {
    if (!this.getSelectedGame) {
      this.$router.push("/");
    }
  },
  head() {
    const name = this.getSelectedGame?.name;
    return {
      title: name,
      meta: [
        {
          hid: `description`,
          name: "description",
          content: `Some description for single game`,
        },
      ],
    };
  },
};
</script>

<style scoped>
img.img {
  width: 100%;
  max-height: 50vh;
  object-fit: cover;
  object-position: top;
  border-radius: 4px;
}
</style>
