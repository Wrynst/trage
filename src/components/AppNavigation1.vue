<!-- <template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app clipped>
      <v-list dense>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-view-dashboard</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Dashboard</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-settings</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Settings</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app clipped-left>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>DeCoin</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <!-- v-col class="shrink" 
          <template>
            <v-toolbar color="orange accent-1">
              <v-app-bar-nav-icon 
                class="hidden-sm-and-down"
              ></v-app-bar-nav-icon>
              <v-toolbar-title class="title mr-6 hidden-sm-and-down"
              >Cryptocurrency</v-toolbar-title
              >
              <v-autocomplete
                v-model="model"
                :items="items"
                :loading="isLoading"
                :search-input.sync="search"
                chips
                clearable
                hide-details
                hide-selected
                item-text="name"
                item-value="symbol"
                label="Search for a coin..."
                solo
              >
                <template v-slot:no-data>
                  <v-list-item>
                    <v-list-item-title>
                      Search for your favorite
                      <strong>Cryptocurrency</strong>
                    </v-list-item-title>
                  </v-list-item>
                </template>
                <template v-slot:selection="{ attr, on, item, selected }">
                  <v-chip
                    v-bind="attr"
                    :input-value="selected"
                    color="blue-grey"
                    class="white--text"
                    v-on="on"
                  >
                    <v-icon left>mdi-coin</v-icon>
                    <span v-text="item.name"></span>
                  </v-chip>
                </template>
                <template v-slot:item="{ item }">
                  <v-list-item-avatar
                    color="indigo"
                    class="headline font-weight-light white--text"
                  >{{ item.name.charAt(0) }}</v-list-item-avatar>
                  <v-list-item-content>
                    <v-list-item-title v-text="item.name"></v-list-item-title>
                    <v-list-item-subtitle v-text="item.symbol"></v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-action>
                    <v-icon>mdi-coin</v-icon>
                  </v-list-item-action>
                </template>
              </v-autocomplete>
              <template v-slot:extension>
                <v-tabs
                  v-model="tab"
                  :hide-slider="!model"
                  color="blue-grey"
                  slider-color="blue-grey"
                >
                  <v-tab :disabled="!model">News</v-tab>
                  <v-tab :disabled="!model">Trading</v-tab>
                  <v-tab :disabled="!model">Blog</v-tab>
                </v-tabs>
              </template>
            </v-toolbar>
          </template>

          <!-- /v-col 
        </v-row>
      </v-container>
    </v-content>

    <v-footer app>
      <span>&copy; 2020</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    isLoading: false,
    items: [],
    model: null,
    search: null,
    tab: null,
    val: null,
    error: null
  }),

  watch: {
    model(val) {
      if (val != null) this.tab = 0;
      else this.tab = null;
    },
    search(val) {
      // Items have already been loaded
      if (this.items.length > 0) return;

      this.isLoading = true;

      // Lazily load input items
      fetch("https://api.coingecko.com/api/v3/coins/list")
        .then(res => res.clone().json())
        .then(res => {
          this.items = res;
        })
        .catch(err => {
          console.log(err);
        })
        .finally(() => (this.isLoading = false));
    },
    created() {
      this.$vuetify.theme.dark = true;
    }
  }
};
</script>
