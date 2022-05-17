<template>
  <div>
    <div class="info-modal" :class="{ hidden: hidden }" ref="info-modal">
      <div class="im-cloud" ref="im-cloud"></div>
      <div class="im-tip"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["position", "booking_data", "hidden"],
  watch: {
    position() {
      const info_modal = this.$refs["info-modal"];
      const im_cloud = this.$refs["im-cloud"];
      const dimensions = info_modal.getBoundingClientRect();

      info_modal.style.left =
        this.position.x_position - dimensions.width / 2 + "px";
      info_modal.style.top =
        this.position.y_position - dimensions.height + "px";
      im_cloud.innerText = this.booking_data;
    },
  },
};
</script>

<style scoped>
.info-modal {
  position: absolute;
  display: flex;
  width: fit-content;
  align-items: center;
  flex-direction: column;
}
.im-cloud {
  width: 100px;
  height: 50px;
  border-radius: 2px;
  border: 1px solid yellowgreen;
  background: yellowgreen;
  color: black;
  display: flex;
  align-items: center;
  justify-content: center;
}
.im-tip {
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-top: 7px solid yellowgreen;
}
.hidden {
  visibility: hidden;
}
</style>