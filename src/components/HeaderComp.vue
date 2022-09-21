<script>
import StorageComp from "../components/StorageComp.vue";
import BestProduct from "../components/BestProduct.vue";
import CardComp from "../components/CardComp.vue";
import DiagramaComp from "../components/DiagramaComp.vue";
// import TableCard from "../components/TableCard.vue";
import ActiveUser from "../components/ActiveUser.vue";
export default {
  data: () => ({
    password: "Password",
    show: false,
    message: "Search",
    marker: true,
    iconIndex: 0,

    drawer: true,
    miniDrawer: false,
    group: null,

    fav: true,
    menu: false,
    hints: true,

    admins: [
      ["Management", "mdi-account-multiple-outline"],
      ["Settings", "mdi-cog-outline"],
    ],
    cruds: [
      ["Create", "mdi-plus-outline"],
      ["Read", "mdi-file-outline"],
      ["Update", "mdi-update"],
      ["Delete", "mdi-delete"],
    ],
    selectedItem: 1,

    items: [
      {
        action: "mdi-calendar",
        items: [
          { title: "Breakfast & brunch" },
          { title: "New American" },
          { title: "Sushi" },
        ],
        title: "Attractions",
      },
      {
        action: "mdi-chat",

        items: [
          { title: "Breakfast & brunch" },
          { title: "New American" },
          { title: "Sushi" },
        ],
        title: "Dining",
      },
      {
        action: "mdi-email",
        items: [{ title: "List Item" }],
        title: "Education",
      },
      {
        action: "mdi-cart",
        items: [{ title: "List Item" }],
        title: "Family",
      },
      {
        action: "mdi-calendar",
        items: [{ title: "List Item" }],
        title: "Health",
      },
      {
        action: "mdi-briefcase",
        items: [{ title: "List Item" }],
        title: "Office",
      },
      {
        action: "mdi-share-variant",
        items: [{ title: "List Item" }],
        title: "Promotions",
      },
    ],
  }),
  computed: {
    icon() {
      return this.icons[this.iconIndex];
    },
  },

  methods: {
    toggleMarker() {
      this.marker = !this.marker;
    },
    sendMessage() {
      this.resetIcon();
      this.clearMessage();
    },
    clearMessage() {
      this.message = "";
    },
    resetIcon() {
      this.iconIndex = 0;
    },
    changeIcon() {
      this.iconIndex === this.icons.length - 1
        ? (this.iconIndex = 0)
        : this.iconIndex++;
    },
  },
  components: {
    CardComp,
    DiagramaComp,
    StorageComp,
    BestProduct,
    // TableCard,
    ActiveUser,
  },
};
</script>

<template>
  <div>
    <v-app>
      <v-main style="background: #edf2f9">
        <v-app-bar clipped-left clipped-right fixed flat color="#edf2f9">
          <v-col cols="2" class="d-flex pa-0">
            <v-app-bar-nav-icon
              @click.stop="miniDrawer = !miniDrawer"
            ></v-app-bar-nav-icon>

            <!-- <div class="ml-3"></div> -->

            <v-img
              lazy-src="https://frlive.prium.me/static/media/falcon.fa3b1ec6.png"
              max-height="40"
              max-width="40"
              src="https://frlive.prium.me/static/media/falcon.fa3b1ec6.png"
            ></v-img>
            <v-toolbar-title
              tag="h4"
              style="
                padding-left: 10px;
                font-weight: 700;
                color: #3473a5;
                font-size: 30px;
                font-family: font-sans-serif;
              "
              >falcon</v-toolbar-title
            >
          </v-col>

          <v-col cols="10">
            <v-row>
              <div id="search" class="ml-2">
                <v-icon size="18px" color="#b6c1d2"> mdi-magnify </v-icon>

                <form>
                  <input
                    type="text"
                    value=""
                    placeholder="Search..."
                    name="q"
                    autocomplete="off"
                    class=""
                  />
                </form>
                <div id="jquery-live-search">
                  <ul id="search-results" class="dropdown"></ul>
                </div>
              </div>

              <v-spacer> </v-spacer>

              <div>
                <v-tooltip bottom>
                  <template v-slot:activator="{ on, attrs }">
                    <v-icon
                      style="
                        background: rgb(235 235 235);
                        border-radius: 50%;
                        width: 34px;
                        height: 34px;
                      "
                      color="primary"
                      dark
                      v-bind="attrs"
                      v-on="on"
                    >
                      mdi-weather-night
                    </v-icon>
                  </template>
                  <span>mdi-weather-night</span>
                </v-tooltip>

                <v-tooltip bottom>
                  <template v-slot:activator="{ on, attrs }">
                    <v-icon color="primary" dark v-bind="attrs" v-on="on">
                      mdi-cart
                    </v-icon>
                  </template>
                  <span>mdi-cart</span>
                </v-tooltip>

                <v-tooltip bottom>
                  <template v-slot:activator="{ on, attrs }">
                    <v-icon color="primary" dark v-bind="attrs" v-on="on">
                      mdi-bell-badge
                    </v-icon>
                  </template>
                  <span>mdi-bell-badge</span>
                </v-tooltip>

                <v-tooltip bottom>
                  <template v-slot:activator="{ on, attrs }">
                    <v-icon color="primary" dark v-bind="attrs" v-on="on">
                      mdi-bell
                    </v-icon>
                  </template>
                  <span>mdi-bell</span>
                </v-tooltip>

                <v-tooltip bottom>
                  <template v-slot:activator="{ on, attrs }">
                    <v-icon color="primary" dark v-bind="attrs" v-on="on">
                      mdi-dots-grid
                    </v-icon>
                  </template>
                  <span>mdi-dots-grid</span>
                </v-tooltip>

                <v-menu
                  v-model="menu"
                  :close-on-content-click="false"
                  :nudge-left="130"
                  :nudge-top="-10"
                  offset-y
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-avatar size="34" v-bind="attrs" v-on="on">
                      <img
                        src="https://cdn.vuetifyjs.com/images/john.jpg"
                        alt="John"
                      /> </v-avatar
                  ></template>

                  <v-card width="170">
                    <v-list>
                      <v-list-item>
                        <v-list-item-avatar>
                          <img
                            src="https://cdn.vuetifyjs.com/images/john.jpg"
                            alt="John"
                          />
                        </v-list-item-avatar>

                        <v-list-item-content>
                          <v-list-item-title>John Leider</v-list-item-title>
                          <v-list-item-subtitle
                            >Founder of Vuetify</v-list-item-subtitle
                          >
                        </v-list-item-content>

                        <v-list-item-action>
                          <v-btn
                            :class="fav ? 'red--text' : ''"
                            icon
                            @click="fav = !fav"
                          >
                            <v-icon>mdi-heart</v-icon>
                          </v-btn>
                        </v-list-item-action>
                      </v-list-item>
                    </v-list>

                    <v-divider></v-divider>

                    <v-list>
                      <v-list-item>
                        <v-list-item-action>
                          <v-switch v-model="message" color="purple"></v-switch>
                        </v-list-item-action>
                        <v-list-item-title>Enable messages</v-list-item-title>
                      </v-list-item>

                      <v-list-item>
                        <v-list-item-action>
                          <v-switch v-model="hints" color="purple"></v-switch>
                        </v-list-item-action>
                        <v-list-item-title>Enable hints</v-list-item-title>
                      </v-list-item>
                    </v-list>

                    <v-card-actions>
                      <v-spacer></v-spacer>

                      <v-btn text @click="menu = false"> Cancel </v-btn>
                      <v-btn color="primary" text @click="menu = false">
                        Save
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-menu>
              </div></v-row
            >
          </v-col>
        </v-app-bar>
        <div class="d-flex" style="padding-top: 65px">
          <div style="height: 100%">
            <v-navigation-drawer
              height="100vh"
              class="rounded"
              color="#232e3c"
              dark
              v-model="drawer"
              :expand-on-hover="miniDrawer"
              :mini-variant="miniDrawer"
              permanent
            >
              <v-list>
                <v-list-group
                  v-for="item in items"
                  :key="item.title"
                  v-model="item.active"
                  :prepend-icon="item.action"
                  :value="true"
                  no-action
                >
                  <template v-slot:activator>
                    <v-list-item-content>
                      <v-list-item-title
                        v-text="item.title"
                      ></v-list-item-title>
                    </v-list-item-content>
                  </template>

                  <v-list-item v-for="child in item.items" :key="child.title">
                    <v-list-item-content>
                      <v-list-item-title
                        v-text="child.title"
                      ></v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-group>
              </v-list>
            </v-navigation-drawer>
          </div>
          <div style="width: 100%">
            <v-row class="mx-auto">
              <v-col cols="3" v-for="item in 4" :key="item.id">
                <DiagramaComp />
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6" v-for="item in 2" :key="item.id">
                <CardComp />
              </v-col>
            </v-row>

            <v-row class="mx-auto">
              <v-col cols="12" v-for="item in 1" :key="item.id">
                <StorageComp />
              </v-col>
            </v-row>
            <v-row class="mx-auto">
              <v-col cols="12" v-for="item in 1" :key="item.id">
                <BestProduct />
              </v-col>
            </v-row>
            <!-- <v-row class="mx-auto">
              <v-col cols="12" v-for="item in 1" :key="item.id">
                <TableCard />
              </v-col>
            </v-row> -->
            <v-row class="mx-auto">
              <v-col cols="12" v-for="item in 1" :key="item.id">
                <ActiveUser />
              </v-col>
            </v-row>
          </div>
        </div>
      </v-main>
    </v-app>
  </div>
</template>

<style lang="scss" scoped>
.language {
  font-weight: 600;
  font-size: 16px;
  color: white;
}
#search {
  margin-top: 1px;
  display: flex;
  align-items: center;
  float: left;
  min-width: 350px;
  border: #d8e2ef 1px solid;
  padding: 4px 14px;
  background-color: #fff;
  border-radius: 30px;
  &:focus {
    border: #0a50bb66 1px solid;
  }
}
#search form {
  position: relative;
}

#search input {
  padding: 0 10px 0 8px;
  color: #555555;
  border: none;
  width: 180px;
  height: 29px;
  overflow: hidden;
}

#search input:hover {
  background-position: 0px -32px;
}
#search input:hover {
  background-position: 0px -32px;
}
textarea:focus,
input:focus {
  outline: none;
}
::placeholder {
  color: #c5c5c5;
  font-weight: 500;
  font-size: 16px;
}
</style>

