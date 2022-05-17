<template>
  <div>
    <div id="lr-container">
      <div
        class="triangle-left"
        :class="{ 'lr-left-stop': stop_left, 'lr-hide': hidden }"
        @click="clickLeft()"
      ></div>
      <span class="lr-month">{{ selected_month }}</span>
      <div
        class="triangle-right"
        :class="{ 'lr-right-stop': stop_right, 'lr-hide': hidden }"
        @click="clickRight()"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["months"],
  data() {
    return {
      month_counter: 0,
      stop_left: true,
      stop_right: false,
      hidden: false,
    };
  },
  computed: {
    selected_month() {
      return this.months[this.month_counter];
    },
  },
  methods: {
    clickLeft() {
      if (this.month_counter > 0) {
        this.month_counter--;
      }
    },
    clickRight() {
      if (this.month_counter < this.months.length - 1) {
        this.month_counter++;
      }
    },
  },
  watch: {
    // enables class binding to give the "disabled" arow different color
    month_counter() {
      this.month_counter === 0
        ? (this.stop_left = true)
        : (this.stop_left = false);
      this.month_counter === this.months.length - 1
        ? (this.stop_right = true)
        : (this.stop_right = false);
      // sends current month index to parrent
      this.$root.$emit("month-change", this.month_counter);
    },
  },
  created() {
    // hides left & right arrows when there is only one month of data
    this.months.length === 1 ? (this.hidden = true) : (this.hidden = false);
  },
};
</script>

<style scoped>
#lr-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.triangle-left {
  width: 0;
  height: 0;
  border-top: 10px solid transparent;
  border-right: 15px solid #555;
  border-bottom: 10px solid transparent;
  /* margin-right: 15px; */
  cursor: pointer;
}
.triangle-right {
  width: 0;
  height: 0;
  border-top: 10px solid transparent;
  border-left: 15px solid #555;
  border-bottom: 10px solid transparent;
  /* margin-left: 15px; */
  cursor: pointer;
}
.lr-month {
  min-width: 100px;
  display: flex;
  justify-content: center;
  /* border: 1px solid yellow; */
}
/* set the color within the variable in App.vue */
.lr-left-stop {
  border-right-color: var(--arrow-color);
  cursor: not-allowed;
}
.lr-right-stop {
  border-left-color: var(--arrow-color);
  cursor: not-allowed;
}
.lr-hide {
  display: none;
}
</style>