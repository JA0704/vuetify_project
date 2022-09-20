<script>
export default {
  data: () => ({
    value: "",
    events: [],
    colors: [
      "#2196F3",
      "#3F51B5",
      "#673AB7",
      "#00BCD4",
      "#4CAF50",
      "#FF9800",
      "#757575",
    ],
    items: ["Foo", "Bar", "Fizz", "Buzz"],
    names: [
      "Meeting",
      "Holiday",
      "PTO",
      "Travel",
      "Event",
      "Birthday",
      "Conference",
      "Party",
    ],
    dragEvent: null,
    dragStart: null,
    createEvent: null,
    createStart: null,
    extendOriginal: null,
  }),
  methods: {
    startDrag({ event, timed }) {
      if (event && timed) {
        this.dragEvent = event;
        this.dragTime = null;
        this.extendOriginal = null;
      }
    },
    startTime(tms) {
      const mouse = this.toTime(tms);

      if (this.dragEvent && this.dragTime === null) {
        const start = this.dragEvent.start;

        this.dragTime = mouse - start;
      } else {
        this.createStart = this.roundTime(mouse);
        this.createEvent = {
          name: `Event #${this.events.length}`,
          color: this.rndElement(this.colors),
          start: this.createStart,
          end: this.createStart,
          timed: true,
        };

        this.events.push(this.createEvent);
      }
    },
    extendBottom(event) {
      this.createEvent = event;
      this.createStart = event.start;
      this.extendOriginal = event.end;
    },
    mouseMove(tms) {
      const mouse = this.toTime(tms);

      if (this.dragEvent && this.dragTime !== null) {
        const start = this.dragEvent.start;
        const end = this.dragEvent.end;
        const duration = end - start;
        const newStartTime = mouse - this.dragTime;
        const newStart = this.roundTime(newStartTime);
        const newEnd = newStart + duration;

        this.dragEvent.start = newStart;
        this.dragEvent.end = newEnd;
      } else if (this.createEvent && this.createStart !== null) {
        const mouseRounded = this.roundTime(mouse, false);
        const min = Math.min(mouseRounded, this.createStart);
        const max = Math.max(mouseRounded, this.createStart);

        this.createEvent.start = min;
        this.createEvent.end = max;
      }
    },
    endDrag() {
      this.dragTime = null;
      this.dragEvent = null;
      this.createEvent = null;
      this.createStart = null;
      this.extendOriginal = null;
    },
    cancelDrag() {
      if (this.createEvent) {
        if (this.extendOriginal) {
          this.createEvent.end = this.extendOriginal;
        } else {
          const i = this.events.indexOf(this.createEvent);
          if (i !== -1) {
            this.events.splice(i, 1);
          }
        }
      }

      this.createEvent = null;
      this.createStart = null;
      this.dragTime = null;
      this.dragEvent = null;
    },
    roundTime(time, down = true) {
      const roundTo = 15; // minutes
      const roundDownTime = roundTo * 60 * 1000;

      return down
        ? time - (time % roundDownTime)
        : time + (roundDownTime - (time % roundDownTime));
    },
    toTime(tms) {
      return new Date(
        tms.year,
        tms.month - 1,
        tms.day,
        tms.hour,
        tms.minute
      ).getTime();
    },
    getEventColor(event) {
      const rgb = parseInt(event.color.substring(1), 16);
      const r = (rgb >> 16) & 0xff;
      const g = (rgb >> 8) & 0xff;
      const b = (rgb >> 0) & 0xff;

      return event === this.dragEvent
        ? `rgba(${r}, ${g}, ${b}, 0.7)`
        : event === this.createEvent
        ? `rgba(${r}, ${g}, ${b}, 0.7)`
        : event.color;
    },
    getEvents({ start, end }) {
      const events = [];

      const min = new Date(`${start.date}T00:00:00`).getTime();
      const max = new Date(`${end.date}T23:59:59`).getTime();
      const days = (max - min) / 86400000;
      const eventCount = this.rnd(days, days + 20);

      for (let i = 0; i < eventCount; i++) {
        const timed = this.rnd(0, 3) !== 0;
        const firstTimestamp = this.rnd(min, max);
        const secondTimestamp = this.rnd(2, timed ? 8 : 288) * 900000;
        const start = firstTimestamp - (firstTimestamp % 900000);
        const end = start + secondTimestamp;

        events.push({
          name: this.rndElement(this.names),
          color: this.rndElement(this.colors),
          start,
          end,
          timed,
        });
      }

      this.events = events;
    },
    rnd(a, b) {
      return Math.floor((b - a + 1) * Math.random()) + a;
    },
    rndElement(arr) {
      return arr[this.rnd(0, arr.length - 1)];
    },
  },
};
</script>

<template>
  <div class="col-12 pt-0">
    <v-card class="card" hover>
      <div class="bg-light card-header">
        <v-row justify="center" align="center">
          <v-col cols="7">
            <v-list style="font-size: 14px" color="#f9fafd" class="mb-3"
              >Running Projects</v-list
            >
          </v-col>
          <v-col cols="col-5 pa-0">
            <v-select
              class="pt-1 pr-2 pb-0"
              :items="items"
              hide-selected
              dense
              outlined
              hide-spin-buttons
              height="10"
            ></v-select>
          </v-col>
        </v-row>
      </div>
      <div class="card-body">
        <div class="align-items-center pt-2 border-bottom border-200 row">
          <div class="pt-1 col">
            <div class="d-flex align-items-center">
              <div class="avatar avatar-xl me-3">
                <div
                  style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    background-color:#e6effc
                    padding: 10px;
                    border-radius: 50%;
                    width: 30px;
                    height: 30px;
                  "
                  class="avatar-name rounded-circle bg-soft-primary"
                >
                  <span
                    class="fs-0 text-primary"
                    style="color: #3289f0; font-weight: 900"
                    >F</span
                  >
                </div>
              </div>
              <div class="d-flex position-relative">
                <p class="d-flex mb-0 text-center" style="align-self: center">
                  <a
                    style="color: black; font-size: 14px"
                    class="text-800 stretched-link"
                    href="#!"
                    >Falcon</a
                  ><span
                    style="
                      font-size: 10px;
                      font-weight: 600;
                      background: #e6effc;
                      padding: 0px 8px;
                      height: 17px;
                    "
                    class="ms-2 text-primary badge rounded-pill bg-200"
                    >90%</span
                  >
                </p>
              </div>
            </div>
          </div>
          <div class="pt-4 col">
            <div
              style="justify-content: end"
              class="justify-content-end align-items-center row"
            >
              <div class="col-auto pe-0">
                <div class="fs--1 fw-semi-bold">58:20:00</div>
              </div>
              <div class="pe-card col-5">
                <v-progress-linear value="15"></v-progress-linear>
              </div>
            </div>
          </div>
        </div>
        <v-divider></v-divider>
        <div class="align-items-center pt-6 pb-2 border-bottom border-200 row">
          <div class="pt-1 col">
            <div class="d-flex align-items-center">
              <div class="avatar avatar-xl me-3">
                <div
                  style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    background-color:#e6effc
                    padding: 10px;
                    border-radius: 50%;
                    width: 30px;
                    height: 30px;
                  "
                  class="avatar-name rounded-circle bg-soft-primary"
                >
                  <span
                    class="fs-0 text-primary"
                    style="color: #3289f0; font-weight: 900"
                    >F</span
                  >
                </div>
              </div>
              <div class="d-flex position-relative">
                <p class="d-flex mb-0 text-center" style="align-self: center">
                  <a
                    style="color: black; font-size: 14px"
                    class="text-800 stretched-link"
                    href="#!"
                    >Falcon</a
                  ><span
                    style="
                      font-size: 10px;
                      font-weight: 600;
                      background: #e6effc;
                      padding: 0px 8px;
                      height: 17px;
                    "
                    class="ms-2 text-primary badge rounded-pill bg-200"
                    >90%</span
                  >
                </p>
              </div>
            </div>
          </div>
          <div class="pt-4 col">
            <div
              style="justify-content: end"
              class="justify-content-end align-items-center row"
            >
              <div class="col-auto pe-0">
                <div class="fs--1 fw-semi-bold">58:20:00</div>
              </div>
              <div class="pe-card col-5">
                <v-progress-linear value="15"></v-progress-linear>
              </div>
            </div>
          </div>
        </div>
        <v-divider></v-divider>
        <div class="align-items-center pt-6 pb-2 border-bottom border-200 row">
          <div class="pt-1 col">
            <div class="d-flex align-items-center">
              <div class="avatar avatar-xl me-3">
                <div
                  style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    background-color:#e6effc
                    padding: 10px;
                    border-radius: 50%;
                    width: 30px;
                    height: 30px;
                  "
                  class="avatar-name rounded-circle bg-soft-primary"
                >
                  <span
                    class="fs-0 text-primary"
                    style="color: #3289f0; font-weight: 900"
                    >F</span
                  >
                </div>
              </div>
              <div class="d-flex position-relative">
                <p class="d-flex mb-0 text-center" style="align-self: center">
                  <a
                    style="color: black; font-size: 14px"
                    class="text-800 stretched-link"
                    href="#!"
                    >Falcon</a
                  ><span
                    style="
                      font-size: 10px;
                      font-weight: 600;
                      background: #e6effc;
                      padding: 0px 8px;
                      height: 17px;
                    "
                    class="ms-2 text-primary badge rounded-pill bg-200"
                    >90%</span
                  >
                </p>
              </div>
            </div>
          </div>
          <div class="pt-4 col">
            <div
              style="justify-content: end"
              class="justify-content-end align-items-center row"
            >
              <div class="col-auto pe-0">
                <div class="fs--1 fw-semi-bold">58:20:00</div>
              </div>
              <div class="pe-card col-5">
                <v-progress-linear value="15"></v-progress-linear>
              </div>
            </div>
          </div>
        </div>
        <v-divider></v-divider>
        <div class="align-items-center pt-6 pb-2 border-bottom border-200 row">
          <div class="pt-1 col">
            <div class="d-flex align-items-center">
              <div class="avatar avatar-xl me-3">
                <div
                  style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    background-color:#e6effc
                    padding: 10px;
                    border-radius: 50%;
                    width: 30px;
                    height: 30px;
                  "
                  class="avatar-name rounded-circle bg-soft-primary"
                >
                  <span
                    class="fs-0 text-primary"
                    style="color: #3289f0; font-weight: 900"
                    >F</span
                  >
                </div>
              </div>
              <div class="d-flex position-relative">
                <p class="d-flex mb-0 text-center" style="align-self: center">
                  <a
                    style="color: black; font-size: 14px"
                    class="text-800 stretched-link"
                    href="#!"
                    >Falcon</a
                  ><span
                    style="
                      font-size: 10px;
                      font-weight: 600;
                      background: #e6effc;
                      padding: 0px 8px;
                      height: 17px;
                    "
                    class="ms-2 text-primary badge rounded-pill bg-200"
                    >90%</span
                  >
                </p>
              </div>
            </div>
          </div>
          <div class="pt-4 col">
            <div
              style="justify-content: end"
              class="justify-content-end align-items-center row"
            >
              <div class="col-auto pe-0">
                <div class="fs--1 fw-semi-bold">58:20:00</div>
              </div>
              <div class="pe-card col-5">
                <v-progress-linear value="15"></v-progress-linear>
              </div>
            </div>
          </div>
        </div>
        <v-divider></v-divider>
        <div class="align-items-center pt-6 pb-2 border-bottom border-200 row">
          <div class="pt-1 col">
            <div class="d-flex align-items-center">
              <div class="avatar avatar-xl me-3">
                <div
                  style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    background-color:#e6effc
                    padding: 10px;
                    border-radius: 50%;
                    width: 30px;
                    height: 30px;
                  "
                  class="avatar-name rounded-circle bg-soft-primary"
                >
                  <span
                    class="fs-0 text-primary"
                    style="color: #3289f0; font-weight: 900"
                    >F</span
                  >
                </div>
              </div>
              <div class="d-flex position-relative">
                <p class="d-flex mb-0 text-center" style="align-self: center">
                  <a
                    style="color: black; font-size: 14px"
                    class="text-800 stretched-link"
                    href="#!"
                    >Falcon</a
                  ><span
                    style="
                      font-size: 10px;
                      font-weight: 600;
                      background: #e6effc;
                      padding: 0px 8px;
                      height: 17px;
                    "
                    class="ms-2 text-primary badge rounded-pill bg-200"
                    >90%</span
                  >
                </p>
              </div>
            </div>
          </div>
          <div class="pt-4 col">
            <div
              style="justify-content: end"
              class="justify-content-end align-items-center row"
            >
              <div class="col-auto pe-0">
                <div class="fs--1 fw-semi-bold">58:20:00</div>
              </div>
              <div class="pe-card col-5">
                <v-progress-linear value="15"></v-progress-linear>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="bg-light p-0 card-footer">
        <a
          style="text-decoration: none"
          role="button"
          tabindex="0"
          href="/#!"
          class="w-100 py-2 btn btn-link btn-sm"
          >Show all projects
        </a>
        <v-icon size="20" color="primary">mdi-chevron-right</v-icon>
      </div>
    </v-card>
  </div>
</template>

<style scoped lang="scss">
a {
  text-decoration: none;
}
.card {
  background-color: #fff;
  padding: 0;
  .card-footer {
    text-align: center;
    background-color: #f9fafd;
    padding: 8px 0;
    a {
      font-size: 14px;
    }
  }
  .card-body {
    background-color: #fff;
    padding: 12px 18px;
    .pe-card {
      align-self: center;
    }
  }
  .card-header {
    background-color: #f9fafd;
    padding: 20px 18px;
    padding-bottom: 0;
  }
}
</style>