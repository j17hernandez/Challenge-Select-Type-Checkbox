<template>
  <div id="app">
    <br /><br />
    <b-container class="app">
      <b-row>
        <b-col v-for="(el, i) in headers" :key="i">
          <b-form-checkbox type="checkbox" v-model="el.value">
            <b-icon :icon="el.icon"></b-icon>
          </b-form-checkbox>
        </b-col>
      </b-row>
      <b-list-group v-if="getItems.length > 0">
        <b-list-group-item v-for="(item, i) in getItems" :key="i">
          <b-row>
            <b-col>
              <b-icon
                :icon="item.icon"
                :variant="getColor(item.value)"
              ></b-icon>
            </b-col>
            <b-col>
              <span> {{ item.title }} </span>
            </b-col>
            <b-col>
              <b-form-input v-model="item.value" type="number"></b-form-input>
            </b-col>
          </b-row>
        </b-list-group-item>
      </b-list-group>
      <span v-else>No selected content</span>
    </b-container>
  </div>
</template>

<script>
  export default {
    name: "App",
    data() {
      return {
        statusPlus: false,
        second: false,
        headers: [
          {
            icon: "plus-circle",
            code: "first",
            value: true,
          },
          {
            icon: "person",
            code: "second",
            value: false,
          },
          {
            icon: "diagram3",
            code: "three",
            value: false,
          },
        ],
        items: [
          {
            icon: "plus-circle",
            title: "box_corners",
            value: 10,
            code: "first",
          },
          {
            icon: "plus-circle",
            title: "box_corners",
            value: 2,
            code: "first",
          },
          {
            icon: "person",
            title: "person",
            value: 34,
            code: "second",
          },
          {
            icon: "person",
            title: "person",
            value: 15,
            code: "second",
          },
          {
            icon: "diagram3",
            title: "diagram",
            value: 34,
            code: "three",
          },
          {
            icon: "diagram3",
            title: "diagram",
            value: 27,
            code: "three",
          },
        ],
      };
    },
    methods: {
      // Function to get the color
      getColor(value) {
        if (value > 0 && value < 10) return "danger";
        else if (value > 10 && value < 20) return "warning";
        else if (value > 20 && value < 30) return "success";
        else return "info";
      },
    },
    computed: {
      // Computed to get items selected
      getItems() {
        const items = [];
        this.headers.forEach((el) => {
          if (el.value) {
            this.items.filter((it) => {
              if (it.code === el.code) {
                return items.push(it);
              }
            });
          }
        });
        return items;
      },
    },
  };
</script>
<style scoped>
  .app {
    align-content: center;
    display: flex;
    flex-direction: column;
  }
</style>
