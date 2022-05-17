<template>
  <div>
    <div class="tbl-container">
      <div class="tbl-header-left">
        <div class="tbl-title child">Calendar view</div>
      </div>

      <!-- Table Header -->
      <div class="tbl-header-right border-bottom">
        <div>
          <!-- Change Month, left, right -->
          <div class="tbl-month">
            <LeftRight :months="months" />
            <!-- <span>October</span> -->
          </div>
          <!-- Table Date -->
          <div class="tbl-dates-row">
            <div v-for="(date, i) in dates" :key="i" class="tbl-date child">
              {{ date }}
            </div>
          </div>
        </div>
      </div>

      <!-- Inventories -->
      <div class="tbl-data">
        <div class="tbl-inventory-data">
          <ul>
            <!-- Inventory list-->
            <template v-for="(inv, i) in inventories">
              <!-- Inventory placement name -->
              <li :key="i">
                <span class="tbl-inventory-name tbl-placement child">{{
                  inv.placement
                }}</span>
                <span class="tbl-squares-row border-left child">
                  <div class="table-square"></div>
                </span>
              </li>
              <!-- Inventory media name -->
              <li v-for="media in inv.media" :key="media.name">
                <span class="tbl-inventory-name tbl-indent child">{{
                  media.name
                }}</span>
                <!-- Square icon -->
                <span class="tbl-squares-row border-left child">
                  <div
                    v-for="(booking, index) in media.bookings"
                    :key="index"
                    class="tbl-square"
                    :class="{
                      'tbl-green': booking === 0,
                      'tbl-orange': booking === 1,
                      'tbl-purple': booking === 2,
                    }"
                  >
                    <span
                      @mouseover="modalPositionAndData($event, booking)"
                      @mouseout="resetModal()"
                      >&#9829;</span
                    >
                  </div>
                </span>
              </li>
            </template>
          </ul>
          <InfoModal
            :position="position"
            :booking_data="booking_data"
            :hidden="hidden_modal"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LeftRight from "./LeftRight";
import InfoModal from "./InfoModal";

export default {
  components: {
    LeftRight,
    InfoModal,
  },
  data() {
    return {
      hidden_modal: true,
      position: {},
      booking_data: {},

      // server data | from response
      months: ["October", "November", "December"],
      /**
       * by switching months BE can send this structure, as we see it now,
       * and sequentially change it for every month (request/response)
       * or
       * send all months at once, in a structure like this: [[], [], []]
       */
      dates: ["01/10", "02/10", "03/10", "04/10"],
      inventories: [
        {
          placement: "Academic Psyhiatry 40596h1",
          media: [
            // booking can be 0, 1 or 2
            { name: "s1 SCH 53003 SCO 26000", bookings: [0, 0, 1, 2] },
            { name: "h2 SCH 53003 SCO 26000", bookings: [0, 1, 1, 2] },
            { name: "c1 SCH 53003 SCO 26000", bookings: [0, 0, 0, 1] },
            { name: "c2 SCH 53003 SCO 26000", bookings: [1, 0, 2, 0] },
          ],
          /**
           * Green  #8CD183 - represents placements with 0 bookings
           * Orange #FF5300 - represents placements with 1 campaign booked on them
           * Purple  #7837E6 - represents placements with 1 or more campaigns booked on them
           *
           * !!! We always see one month of data? Will pagination relate to that to?
           * !!! TAG explanation needed!
           */
        },
        {
          placement: "Academic Questions 12129",
          media: [
            { name: "h1 SCO 36000 SCO 38000", bookings: [1, 2, 1, 0] },
            { name: "h2 SCO 36000 SCO 38000", bookings: [0, 1, 2, 0] },
            { name: "c1 SCO 36000 SCO 38000", bookings: [1, 0, 0, 1] },
            { name: "c2 SCO 36000 SCO 38000", bookings: [2, 0, 1, 2] },
          ],
        },
      ],
    };
  },
  methods: {
    modalPositionAndData(e, booking) {
      this.hidden_modal = false;
      const element_dimensions = e.target.getBoundingClientRect();
      this.position = Object.assign({}, this.position, {
        x_position: element_dimensions.left + element_dimensions.width / 2,
        y_position: element_dimensions.top,
      });
      this.booking_data = booking;
    },
    resetModal() {
      this.hidden_modal = true;
    },
  },
  mounted() {
    // reacting to event from LeftRight.vue component, which is sending index of a current month
    this.$root.$on("month-change", (payload) => {
      console.log(payload);
    });
  },
};
</script>

<style scoped>
.tbl-container {
  border: 1px solid red;
  color: white;
  display: flex;
  flex-wrap: wrap;
}

/* centering left text, Layout names, handling ellipsis */
.child {
  box-sizing: border-box;
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.tbl-header-left {
  width: 20%;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  /* align-items: center; */
  /* border: 1px solid yellow; */
}
.tbl-header-right {
  width: 80%;
}

.tbl-month {
  margin: 0 auto;
}

.tbl-data {
  width: 100%;
}
.tbl-inventory-name {
  width: 20%;
}
.tbl-inventory-data {
  width: 100%;
  /* border: 1px solid yellow; */
}

.tbl-placement {
  font-weight: bold;
}

.tbl-dates-row {
  height: auto;
  padding: 2px 0;
  display: flex;
  align-items: center;
  /* border: 1px solid gray; */
}
.tbl-date {
  flex-grow: 1;
  font-size: 16px;
  /* border: 1px solid rgb(126, 119, 103); */
}

.tbl-squares-row {
  width: 80%;
  display: flex;
  align-items: center;
}
.tbl-square {
  flex-grow: 1;
}
.tbl-square span:hover {
  color: aqua;
  cursor: pointer;
}
/* colors */
.tbl-green {
  color: #8CD183;
}
.tbl-orange {
  color: #FF5300;
}
.tbl-purple {
  color: #7837E6;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  display: flex;
}
.tbl-indent {
  text-indent: 20px;
}

.border-bottom {
  border-bottom: 1px solid green;
}
.border-left {
  border-left: 1px solid green;
}
</style>