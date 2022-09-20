<template>
  <v-row class="mb-3">
    <v-col cols="8">
      <v-card class="pt-5 pb-5" hover>
        <div class="h-lg-100 card">
          <div class="d-flex align-items-center card-body">
            <div style="width: 100%">
              <h5 class="mb-3 text-800">
                Using Storage <strong class="text-dark">1466 MB </strong>of 2 GB
              </h5>
              <div class="d-flex" style="border-radius: 4px; overflow: hidden">
                <v-progress-linear
                  color="#2c7be5"
                  value="100"
                  height="10"
                ></v-progress-linear>
                <br />
                <v-progress-linear
                  color="#27bcfd"
                  value="100"
                  height="10"
                ></v-progress-linear>
                <br />
                <v-progress-linear
                  color="#00d27a"
                  value="100"
                  height="10"
                ></v-progress-linear>
                <br />
                <v-progress-linear
                  color="#9da9bb"
                  value="100"
                  height="10"
                ></v-progress-linear>
              </div>
              <div class="fs--1 fw-semi-bold text-500 row">
                <div class="d-flex align-items-center pe-2 col-auto">
                  <v-badge color="#2c7be5" dot inline left></v-badge>
                  <span style="color: #9da9bb; font-size: 14px"
                    >Regular (895MB)</span
                  >
                </div>
                <div class="d-flex align-items-center pe-2 col-auto">
                  <v-badge color="#27bcfd" dot inline left></v-badge>
                  <span style="color: #9da9bb; font-size: 14px"
                    >System (379MB)</span
                  >
                </div>
                <div class="d-flex align-items-center pe-2 col-auto">
                  <v-badge color="#00d27a" dot inline left></v-badge>
                  <span style="color: #9da9bb; font-size: 14px"
                    >Shared (192MB)</span
                  >
                </div>
                <div class="d-flex align-items-center pe-2 col-auto">
                  <v-badge color="#9da9bb" dot inline left></v-badge>
                  <span style="color: #9da9bb; font-size: 14px"
                    >Free (576MB)</span
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </v-card></v-col
    >
    <v-col cols="4">
      <v-card class="pb-2" hover>
        <div class="overflow-hidden undefined card">
          <div
            class="bg-holder p-card bg-card"
            style="background-image: url('/static/media/corner-1.44e8a57b.png')"
          ></div>
          <div class="position-relative card-body">
            <h3 class="text-warning" style="color: #f6884b">
              Running out of your space?
            </h3>
            <p class="fs--1 mb-0" style="color: #afb7c1; font-size: 12px">
              Your storage will be running out soon. Get more<br />
              space and powerful productivity features.
            </p>
            <v-content class="mt-5">
              <a role="button" tabindex="0" href="/#!" class="btn btn-link"
                ><span style="color: #f6884b">Upgrade storage</span>
              </a>
              <v-icon color="#f6884b">mdi-chevron-right</v-icon></v-content
            >
          </div>
        </div>
      </v-card></v-col
    >
  </v-row>
</template>

<style  scoped>
a {
  text-decoration: none;
}
</style> 
  
