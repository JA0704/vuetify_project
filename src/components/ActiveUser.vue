<template>
  <v-row>
    <v-col cols="3">
      <v-card class="mx-auto pb-0" hover rounded>
        <v-list subheader>
          <div
            class="d-flex align-center pt-2 pb-1 pl-6 pr-3"
            style="background: #f9fafd"
          >
            <v-card color="#f9fafd" flat>Active Users </v-card>
            <v-spacer> </v-spacer>
            <v-menu bottom left>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  style="box-shadow: none"
                  color="#f9fafd"
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon size="18" color="#748194" tile
                    >mdi-dots-horizontal</v-icon
                  >
                </v-btn>
              </template>
              <v-list>
                <v-list-item v-for="(item, index) in items" :key="index">
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </div>

          <v-list-item v-for="chat in recent" :key="chat.title">
            <v-list-item two-line class="pl-0">
              <v-badge
                bordered
                bottom
                color="deep-purple accent-4"
                offset-x="10"
                offset-y="10"
              >
                <v-avatar size="50">
                  <v-img
                    src="https://cdn.vuetifyjs.com/images/lists/2.jpg"
                  ></v-img>
                </v-avatar>
              </v-badge>
              <div class="mx-2"></div>
              <v-list-item-content class="pt-8">
                <v-list-item-title
                  style="
                    font-weight: 600;
                    font-family: Poppins, -apple-system, BlinkMacSystemFont,
                      Segoe UI, Roboto, Helvetica Neue, Arial, sans-serif,
                      Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol;
                    font-size: 14px;
                  "
                  >Emma Watson</v-list-item-title
                >
                <v-list-item-subtitle style="font-size: 12px"
                  >Admin</v-list-item-subtitle
                >
              </v-list-item-content>
            </v-list-item>
          </v-list-item>
        </v-list>
        <v-list color="#f9fafd" style="text-align: center; cursor: pointer"
          ><span style="color: #2c7be5">All active users</span>
          <v-icon size="18" color="#2c7be5">mdi-chevron-right</v-icon>
        </v-list>
      </v-card></v-col
    >
    <v-col cols="6">
      <v-card class="mx-auto pb-0" hover rounded>
        <v-list subheader>
          <div
            class="d-flex align-center pt-2 pb-1 pl-6 pr-3"
            style="background: #f9fafd"
          >
            <v-card
              color="#f9fafd"
              style="
                font-family: Poppins, -apple-system, BlinkMacSystemFont,
                  Segoe UI, Roboto, Helvetica Neue, Arial, sans-serif,
                  Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol;
                font-weight: 500;
              "
              flat
              >Top Products
            </v-card>
            <v-spacer> </v-spacer>

            <v-list color="#f9fafd" style="text-align: center; cursor: pointer"
              ><span style="color: #2c7be5">View Details</span>
            </v-list>

            <v-menu bottom left>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  style="box-shadow: none"
                  color="#f9fafd"
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon size="18" color="#748194" tile
                    >mdi-dots-horizontal</v-icon
                  >
                </v-btn>
              </template>
              <v-list>
                <v-list-item v-for="(item, index) in items" :key="index">
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </div>

          <v-row class="fill-height">
            <v-col>
              <v-sheet height="64">
                <v-toolbar flat>
                  <v-list
                    style="border: none"
                    outlined
                    class="mr-4"
                    @click="setToday"
                  >
                    <v-badge color="#2c7be5" dot inline left></v-badge>
                    <span style="font-size: 14px">2019</span>
                  </v-list>
                  <v-list
                    style="border: none"
                    outlined
                    class="mr-4"
                    @click="setToday"
                  >
                    <v-badge color="#d8e2ef" dot inline left></v-badge>
                    <span style="font-size: 14px">2018</span>
                  </v-list>
                </v-toolbar>
              </v-sheet>
              <v-sheet height="280px">
                <v-calendar
                  ref="calendar"
                  v-model="focus"
                  color="primary"
                  type="category"
                  category-show-all
                  :categories="categories"
                  :events="events"
                  :event-color="getEventColor"
                  @change="fetchEvents"
                ></v-calendar>
              </v-sheet>
            </v-col>
          </v-row>
        </v-list>
      </v-card>
    </v-col>
    <v-col cols="3"
      ><v-card class="mx-auto" hover rounded>
        <v-list subheader>
          <div
            class="d-flex align-center pt-2 pb-1 pl-6 pr-3"
            style="background: #f9fafd"
          >
            <v-card color="#f9fafd" flat>Active Users </v-card>
            <v-spacer> </v-spacer>
            <v-menu bottom left>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  style="box-shadow: none"
                  color="#f9fafd"
                  dark
                  v-bind="attrs"
                  v-on="on"
                >
                  <v-icon size="18" color="#748194" tile
                    >mdi-dots-horizontal</v-icon
                  >
                </v-btn>
              </template>
              <v-list>
                <v-list-item v-for="(item, index) in items" :key="index">
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </div>

          <div class="text-center">
            <v-progress-circular
              :rotate="360"
              :size="150"
              :width="10"
              :value="value"
              color="blue"
            >
              {{ value }}
            </v-progress-circular>

            <v-list
              style="
                font-size: 16px;
                font-family: Poppins, -apple-system, BlinkMacSystemFont,
                  Segoe UI, Roboto, Helvetica Neue, Arial, sans-serif,
                  Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol;
                font-weight: 500;
              "
              ><v-icon color="#00d27a">mdi-check-bold</v-icon> 35.75 GB
              saved</v-list
            >

            <v-list
              ><span style="color: #5e6e82">38.44 GB total bandwidth</span>
            </v-list>
          </div>
        </v-list>
        <div class="d-flex align-center" style="background: #f9fafd">
          <div style="width: 200px">
            <v-row align="center">
              <v-col class="d-flex" cols="12" sm="10">
                <v-select
                  append-icon="mdi-chevron-down"
                  :items="items"
                  label="Outlined style"
                  dense
                  outlined
                >
                </v-select> </v-col
            ></v-row>
          </div>
          <a
            class="link"
            href="http://"
            target="_blank"
            rel="noopener noreferrer"
            >Help</a
          >
        </div>
      </v-card></v-col
    >
  </v-row>
</template>

<style scoped>
.link {
  text-decoration: none;
}
.link:hover {
  text-decoration: underline;
}
.v-select input {
  display: none;
}
</style>

<script>
export default {
  data: () => ({
    recent: [
      {
        active: true,
        avatar: "https://cdn.vuetifyjs.com/images/lists/1.jpg",
        title: "Jason Oner",
      },
      {
        active: true,
        avatar: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
        title: "Mike Carlson",
      },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/3.jpg",
        title: "Cindy Baker",
      },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/4.jpg",
        title: "Ali Connors",
      },
    ],
    previous: [
      {
        title: "Travis Howard",
        avatar: "https://cdn.vuetifyjs.com/images/lists/5.jpg",
      },
    ],
    items: ["Foo", "Bar", "Fizz", "Buzz"],

    interval: {},
    value: 0,
  }),
  beforeDestroy() {
    clearInterval(this.interval);
  },
  mounted() {
    this.interval = setInterval(() => {
      if (this.value === 100) {
        return (this.value = 0);
      }
      this.value += 10;
    }, 1000);
  },
};
</script>