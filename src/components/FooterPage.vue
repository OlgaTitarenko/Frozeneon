<template>
  <v-footer dark class="footer" >
    <v-card class="flex" flat tile>
      <v-card-title >
        <strong class="subheading">Look at my profile on github</strong>

        <v-spacer></v-spacer>
        <a
          href="https://github.com/OlgaTitarenko"
          target="_blank"
          rel="noopener noreferrer"
        >
          <v-btn class="mx-4" dark icon>
            <v-icon size="24px">
              {{ "mdi-github" }}
            </v-icon>
          </v-btn>
        </a>
      </v-card-title>

      <v-card-text class="py-2 white--text text-center">
        {{ new Date().getFullYear() }} — <strong>Olga Titarenko</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>
<script>
export default {
  name: "FooterPage",
};
</script>

<style scoped>
a {
  text-decoration: none;
}
.footer {
  position: absolute;
  bottom: 0;
  width: 100vw;
  left: 0;
}
</style>