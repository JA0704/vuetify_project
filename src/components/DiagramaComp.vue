<script>
export default {
  data: () => ({
    labels: ["12am", "3am", "6am", "9am", "12pm", "3pm", "6pm", "9pm"],
    value: [200, 675, 410, 390, 310, 460, 250, 240],
  }),
};
</script>

<template>
  <div class="col4">
    <v-card class="h-md-100 card" hover rounded="true">
      <div class="pb-0 card-header">
        <h5 class="mb-0 mt-2">
          Weekly Sales<span
            ><v-icon
              style="
                border: 1px solid #cfd3d9;
                border-radius: 50%;
                margin-left: 6px;
                padding: 1px;
              "
              size="10px "
              >mdi-help</v-icon
            >
          </span>
        </h5>
      </div>
      <div class="d-flex justify-content-between align-items-end card-body">
        <div>
          <h2
            style="color: #5e6e82; font-weight: 400; font-size: 33px"
            class="mb-1 text-700 fw-normal lh-1"
          >
            $47K
          </h2>
          <div
            style="
              font-size: 10px;
              font-weight: 600;
              background: #e6effc;
              padding: 0px 8px;
              height: 17px;
              width: max-content;
            "
            class="rounded-pill"
          >
            +3.5%
          </div>
        </div>
        <div
          class="echarts-for-react"
          _echarts_instance_="ec_1663660518361"
          size-sensor-id="1"
          style="
            height: 60px;
            width: 8.5rem;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
            position: relative;
          "
        >
          <div
            style="
              position: relative;
              width: 136px;
              height: 60px;
              padding: 0px;
              margin: 0px;
              border-width: 0px;
              cursor: pointer;
            "
          >
            <div class="ml-10">
              <v-sparkline
                :value="value"
                :gradient="gradient"
                :smooth="radius || false"
                :padding="padding"
                :line-width="width"
                :stroke-linecap="lineCap"
                :gradient-direction="gradientDirection"
                :fill="fill"
                :type="type"
                :auto-line-width="autoLineWidth"
                auto-draw
              ></v-sparkline>
            </div>
          </div>
          <div
            class=""
            style="
              position: absolute;
              display: block;
              border-style: solid;
              white-space: nowrap;
              z-index: 9999999;
              box-shadow: rgba(0, 0, 0, 0.2) 1px 2px 10px;
              background-color: rgb(249, 250, 253);
              border-width: 1px;
              border-radius: 4px;
              color: rgb(11, 23, 39);
              font: 14px / 21px 'Microsoft YaHei';
              padding: 7px 10px;
              top: 0px;
              left: 0px;
              transform: translate3d(-22px, 0px, 0px);
              border-color: rgb(216, 226, 239);
              pointer-events: none;
              visibility: hidden;
              opacity: 0;
            "
          >
            Thu : 4500
          </div>
        </div>
      </div>
    </v-card>
  </div>
</template>

<style>
.v-sheet--offset {
  top: -24px;
  position: relative;
}
.card {
  background-color: #fff;
  padding: 20px;
}
</style>