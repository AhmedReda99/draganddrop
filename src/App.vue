<template>
  <div style="width:100%;height:2000px;">
    <div class="layoutJSON">
      Displayed as <code>[x, y, w, h]</code>:
      <div class="columns">
        <div v-for="item in layout">
          <b>{{ item.i }}</b
          >: [{{ item.x }}, {{ item.y }}, {{ item.w }}, {{ item.h }}]
        </div>
      </div>
    </div>
    <hr />
    <input type="checkbox" v-model="draggable" /> Draggable
    <input type="checkbox" v-model="resizable" /> Resizable
    <input type="checkbox" v-model="responsive" /> Responsive
    <br />
    <div style="width:100%;overflow-x:scroll">
      <div style="width:100%;margin-top: 10px;height:100%;">
        <grid-layout
          :layout.sync="layout"
          :col-num="12"
          :row-height="30"
          :is-draggable="draggable"
          :is-resizable="resizable"
          :responsive="responsive"
          :vertical-compact="false"
          :prevent-collision="true"
          :use-css-transforms="true"
          :max-rows="users.length + 1"
        >
          <grid-item
            id="fixedclass"
            v-for="item in layout.filter(filterDate)"
            :static="item.static"
            :max-h="1"
            :x="item.x"
            :y="item.y"
            :w="item.w"
            :h="item.h"
            :i="item.i"
            :key="item.i"
          >
            <span v-if="item.y == 0" class="text">{{ item.i }}</span>
          </grid-item>

          <grid-item
            v-for="item in layout.filter(filterEvent)"
            :static="item.static"
            :max-h="1"
            :x="item.x"
            :y="item.y"
            :w="item.w"
            :h="item.h"
            :i="item.i"
            :key="item.i"
          >
          </grid-item>

          <grid-item
            v-for="item in layout.filter(filterUser)"
            :static="item.static"
            :max-h="1"
            :x="item.x"
            :y="item.y"
            :w="item.w"
            :h="item.h"
            :i="item.i"
            :key="item.i"
          >
            <span v-if="item.x == 0" class="text">{{ item.fullname }}</span>
          </grid-item>
        </grid-layout>
      </div>
    </div>
  </div>
</template>

<script>
import { GridLayout, GridItem } from "vue-grid-layout";
export default {
  name: "HelloWorld",
  components: {
    GridLayout,
    GridItem,
  },
  data() {
    return {
      draggable: true,
      resizable: false,
      responsive: false,
      index: 0,
      // usersLayout: [],
      // datesLayout: [],
      layout: [
        // {"x":0,"y":0,"w":1,"h":1,"i":"0", static: true},
        // {"x":1,"y":0,"w":1,"h":1,"i":"1", static: true},
        // {"x":2,"y":0,"w":1,"h":1,"i":"2", static: true},
        // {"x":3,"y":0,"w":1,"h":1,"i":"3", static: true},
        // {"x":4,"y":0,"w":1,"h":1,"i":"4", static: true},
        // {"x":5,"y":0,"w":1,"h":1,"i":"5", static: true},
        // {"x":0,"y":1,"w":1,"h":1,"i":"6", static: true},
        // {"x":0,"y":2,"w":1,"h":1,"i":"7", static: true},
        // {"x":0,"y":3,"w":1,"h":1,"i":"8", static: true},
        // {"x":0,"y":4,"w":1,"h":1,"i":"9", static: true},
        // { x: 0, y: 5, w: 1, h: 1, i: "10", static: true },
        { x: 10, y: 4, w: 1, h: 1, i: "11", static: false },
        // { x: 0, y: 10, w: 1, h: 1, i: "12", static: false },
        { x: 2, y: 10, w: 1, h: 1, i: "13", static: false },
        { x: 4, y: 8, w: 1, h: 1, i: "14", static: false },
        { x: 6, y: 8, w: 1, h: 1, i: "15", static: false },
        { x: 8, y: 10, w: 1, h: 1, i: "16", static: false },
        { x: 10, y: 4, w: 1, h: 1, i: "17", static: false },
        // { x: 0, y: 9, w: 1, h: 1, i: "18", static: false },
        { x: 2, y: 6, w: 1, h: 1, i: "19", static: false },
      ],
      dates: [
        {
          wo_id: "97",
          ps_date_entry: "2017-07-07",
        },
        {
          wo_id: "68",
          ps_date_entry: "2018-09-01",
        },
        {
          wo_id: "68",
          ps_date_entry: "2018-09-01",
        },
        {
          wo_id: "68",
          ps_date_entry: "2018-09-01",
        },
        {
          wo_id: "68",
          ps_date_entry: "2018-09-01",
        },
        {
          wo_id: "68",
          ps_date_entry: "2018-09-01",
        },
      ],
      users: [
        {
          wo_id: "97",
          wo_contact: "73992",
          ps_location: "1",
          lo_city: "Bordeaux",
          co_name: "Maury",
          co_firstname: "Romain",
          co_mail: "rmaury@dawan.fr",
          ps_date_entry: "2017-07-07",
          ps_date_exit: "0000-00-00",
          wo_group: "bordeaux graphisme formateurs pao cao",
          wo_planningorder: "0",
          wo_skills: "",
        },
        {
          wo_id: "68",
          wo_contact: "38754",
          ps_location: "3",
          lo_city: "Lyon",
          co_name: "Nguyen",
          co_firstname: "Valentin",
          co_mail: "vnguyen@dawan.fr",
          ps_date_entry: "2018-09-01",
          ps_date_exit: "0000-00-00",
          wo_group: "Formateurs Lyon Linux Autodesk systemes devops it manager",
          wo_planningorder: "0",
          wo_skills:
            "Windows Server, Linux, VMware, CISCO, Reseaux, PHP, Python, LPI, Docker, Vagrant, DevOps",
        },
        {
          wo_id: "68",
          wo_contact: "38754",
          ps_location: "3",
          lo_city: "Lyon",
          co_name: "Ahmed",
          co_firstname: "Ahmed",
          co_mail: "vnguyen@dawan.fr",
          ps_date_entry: "2018-09-01",
          ps_date_exit: "0000-00-00",
          wo_group: "Formateurs Lyon Linux Autodesk systemes devops it manager",
          wo_planningorder: "0",
          wo_skills:
            "Windows Server, Linux, VMware, CISCO, Reseaux, PHP, Python, LPI, Docker, Vagrant, DevOps",
        },
      ],
    };
  },
  mounted() {
    this.usersAsY();
    this.dateAsX();
  },
  methods: {
    filterUser(e) {
      return e.x === 0;
    },
    filterEvent(e) {
      return e.x > 0 && e.y > 0;
    },
    filterDate(e) {
      return e.y === 0;
    },
    usersAsY() {
      const i = 1;
      this.users.forEach((u) => {
        u.fullname = u.co_firstname + " " + u.co_name;
        console.log(u.fullname);
        u.y = this.users.indexOf(u) + i;
        u.x = 0;
        u.i = u.fullname;
        u.h = 1;
        u.w = 2;
        u.static = true;
        this.layout.push(u);
      });
      //{"x":0,"y":10,"w":1,"h":1,"i":"12", static: false},
    },
    dateAsX() {
      const i = 1;
      this.dates.forEach((d) => {
        d.y = 0;
        d.x = this.dates.indexOf(d) + i;
        d.i = this.dates.indexOf(d) + 1;
        d.h = 1;
        d.w = 1;
        d.static = true;
        this.layout.push(d);
        console.log(this.datesLayout);
      });
      //{"x":0,"y":10,"w":1,"h":1,"i":"12", static: false},
    },
  },
};
</script>

<style scoped>
.vue-grid-layout {
  background: #eee;
}
.vue-grid-item:not(.vue-grid-placeholder) {
  background: rgb(70, 70, 241);
  border: 1px solid black;
  border-radius: 25px;
  color: white;
}
.vue-grid-item .resizing {
  opacity: 0.9;
}
.vue-grid-item .static {
  background: #cce;
}
.vue-grid-item .text {
  font-size: 24px;
  text-align: center;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  height: 100%;
  width: 100%;
}
#fixedclass {
  position: fixed;
  left: 0;
}
.vue-grid-item.vue-grid-placeholder {
  background: s;
  opacity: 0.2;
  transition-duration: 100ms;
  z-index: 2;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
}

.vue-grid-item .no-drag {
  height: 100%;
  width: 100%;
}
.vue-grid-item .minMax {
  font-size: 12px;
}
.vue-grid-item .add {
  cursor: pointer;
}
.vue-draggable-handle {
  position: absolute;
  width: 20px;
  height: 20px;
  top: 0;
  left: 0;
  background: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='10' height='10'><circle cx='5' cy='5' r='5' fill='#999999'/></svg>")
    no-repeat;
  background-position: bottom right;
  padding: 0 8px 8px 0;
  background-repeat: no-repeat;
  background-origin: content-box;
  box-sizing: border-box;
  cursor: pointer;
}
.layoutJSON {
  background: #ddd;
  border: 1px solid black;
  margin-top: 10px;
  padding: 10px;
}
.columns {
  -moz-columns: 120px;
  -webkit-columns: 120px;
  columns: 120px;
}
</style>
