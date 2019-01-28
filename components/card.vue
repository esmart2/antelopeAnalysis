<template>
  <div id="e3" style="max-width: 400px; margin: auto;" class="grey lighten-3">
    <v-container fluid style="min-height: 0;" grid-list-lg>
      <v-layout row wrap></v-layout>
      <v-flex xs12>
        <v-card color="blue" class="white--text">
          <v-layout row>
            <v-flex xs7>
              <v-card-title primary-title>
                <div>
                  <div class="headline">{{names}}</div>
                  <div>From: {{continents}}</div>
                  <div>Weight: {{weights}}</div>
                  <div>Height: {{heights}}</div>
                  <div>Horns: {{horn}}</div>
                </div>
              </v-card-title>
            </v-flex>
            <v-flex xs5>
              <v-img :src="pictures" height="125px" contain></v-img>
            </v-flex>
          </v-layout>
        </v-card>
      </v-flex>
    </v-container>
  </div>
</template>
<script>
export default {
  props: ["names", "continents", "weights", "heights", "horn", "pictures"]
};
</script>
