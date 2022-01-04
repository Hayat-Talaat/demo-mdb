<template>
  <mdb-container class="mt-5">
    <mdb-row>
      <section class="demo-section">
        <div class="light-blue-skin">
          <mdb-side-nav
            slim
            :isCollapsed="collapseD"
            name="New User"
            :OpenedFromOutside.sync="toggleD"
            logo="https://mdbootstrap.com/img/Photos/Avatars/img%20(10).jpg"
            logoRound
            right
            hidden
            :sideNavStyle="{
              zIndex: 1050,
              backgroundColor: '#3e434e',
              color: '#000 !important',
            }"
            style="width:500px !important"
          >
            <!-- Form -->
            <mdb-container>
              <section>
                <mdb-input outline type="text" label="Name" />
                <mdb-input outline type="text" label="Email" />
                <mdb-date-picker-2
                  inline
                  v-model="date20"
                  label="Inline example"
                />
                <mdb-time-picker2
                  placeholder="Select your time"
                  label="format: 24h"
                  :hours-format="24"
                  v-model="picker1"
                />

                <mdb-input
                  type="radio"
                  id="option1-1"
                  name="option1"
                  radioValue="option1"
                  label="Option 1"
                  v-model="radio"
                />
                <mdb-input
                  type="radio"
                  id="option1-2"
                  name="option1"
                  radioValue="option2"
                  label="Option 2"
                  v-model="radio"
                />
                <mdb-input
                  type="radio"
                  id="option1-3"
                  name="option1"
                  radioValue="option3"
                  label="Option 3"
                  v-model="radio"
                />
                <mdb-input
                  type="checkbox"
                  id="checkbox1"
                  label="Default checkbox"
                  class="mb-2 pl-0"
                />
              </section>
              <div>
                <mdb-btn
                  type="button"
                  gradient="blue"
                  rounded
                  class="btn-block z-depth-1a "
                  >Add New User</mdb-btn
                >
              </div>
            </mdb-container>
          </mdb-side-nav>
        </div>
      </section>
    </mdb-row>

    <section class="demo-section">
      <div class="d-flex justify-content-between align-items-center pb-4">
        <h4 class="mb-0">Datatable with other JSON data structure</h4>
        <mdb-btn
          @click="toggleSideNav('D')"
          @keyup.enter="toggleSideNav('D')"
          tabindex="0"
          color="info"
          rounded
          >Add Nwe Item</mdb-btn
        >
      </div>

      <section>
        <mdb-datatable :data="data" striped bordered arrows :display="3" />
      </section>
    </section>
  </mdb-container>
</template>

<script>
import {
  mdbDatatable,
  mdbContainer,
  mdbRow,
  mdbSideNav,
  waves,
  mdbBtn,
  mdbInput,
  mdbDatePicker2,
  mdbTimePicker2,
} from "mdbvue";

export default {
  components: {
    mdbDatatable,
    mdbContainer,
    mdbRow,
    mdbBtn,
    mdbSideNav,
    mdbInput,
    mdbDatePicker2,
    mdbTimePicker2,
  },
  data() {
    return {
      sidenavClass: "black",
      columns: [],
      rows: [],
      toggleA: false,
      toggleB: false,
      toggleC: false,
      toggleD: false,
      collapseC: false,
      collapseD: false,
    };
  },
  computed: {
    data() {
      return {
        columns: this.columns,
        rows: this.rows,
      };
    },
  },
  methods: {
    filterData(dataArr, keys) {
      let data = dataArr.map((entry) => {
        let filteredEntry = {};
        keys.forEach((key) => {
          if (key in entry) {
            filteredEntry[key] = entry[key];
          }
        });
        return filteredEntry;
      });
      return data;
    },

    toggleSideNav(sn) {
      this[`toggle${sn}`] = !this[`toggle${sn}`];
    },
    toggleSlimC() {
      this.collapseC = !this.collapseC;
    },
    toggleSlimD() {
      this.collapseD = !this.collapseD;
    },
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.json())
      .then((json) => {
        let keys = ["id", "title", "completed"];
        let entries = this.filterData(json, keys);
        //columns
        this.columns = keys.map((key) => {
          return {
            label: key.toUpperCase(),
            field: key,
            sort: "asc",
          };
        });
        //rows
        entries.map((entry) => this.rows.push(entry));
      });
  },
  mixins: [waves],
};
</script>

<style>
.side-nav {
  width: 30rem !important;
}
.sideNav {
  background: black;
}
</style>
