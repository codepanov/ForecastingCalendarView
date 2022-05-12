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
            <span>October</span>
          </div>
          <!-- Dates area | number of dates must match number of squares in Squares area -->
          <div class="tbl-dates-row">
            <div class="tbl-date child">01/10</div>
            <div class="tbl-date child">02/10</div>
          </div>
        </div>
      </div>

      <!-- Table Date -->
      <div class="tbl-data">
        <div class="tbl-inventory-data">
          <ul>
            <li>
              <!-- Inventory name -->
              <span class="tbl-inventory-name child">Left part</span>
              <!-- Squares area -->
              <span class="sp-right child border-left tbl-squares-row">
                <div class="tbl-square">&#9829;</div>
                <div class="tbl-square">&#9829;</div>
              </span>
            </li>
            <li>
              <!-- Inventory name -->
              <span class="tbl-inventory-name child">Left part</span>
              <!-- Squares area -->
              <span class="sp-right child border-left tbl-squares-row">
                <div class="tbl-square">&#9829;</div>
                <div class="tbl-square">&#9829;</div>
              </span>
            </li>
            <li>
              <!-- Inventory name -->
              <span class="tbl-inventory-name child">Left part</span>
              <!-- Squares area -->
              <span class="sp-right child border-left tbl-squares-row">
                <div class="tbl-square">&#9829;</div>
                <div class="tbl-square">&#9829;</div>
              </span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dates: ["01/10", "02/10", "03/10", "04/10"],
      inventories: [
        {
          placement: "Academic Psyhiatry 40596h1",
          media_names: [
            "s1 SCH 53003 SCO 26000",
            "h2 SCH 53003 SCO 26000",
            "c1 SCH 53003 SCO 26000",
            "c2 SCH 53003 SCO 26000",
          ],
          bookings: [
            0,
            0,
            1,
            2, // can be 0, 1 or 2
          ],
          /**
           * Green  #8CD183 - represents placements with 0 bookings
           * Orange #FF5300 - represents placements with 1 campaign booked on them
           * Purple  #7837E6 - represents placements with 1 or more  campaigns booked on them
           */
        },
        {
          placement: "Academic Questions 12129",
          media_names: [
            "h1 SCO 36000 SCO 38000",
            "h2 SCO 36000 SCO 38000",
            "c1 SCO 36000 SCO 38000",
            "c2 SCO 36000 SCO 38000",
          ],
          bookings: [1, 2, 1, 1],
        },
      ],
    };
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
}

.sp-right {
  width: 80%;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  display: flex;
}

.border-bottom {
  border-bottom: 1px solid green;
}
.border-left {
  border-left: 1px solid green;
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
  display: flex;
  align-items: center;
}
.tbl-square {
  color: red;
  flex-grow: 1;
}
</style>