<template>
  <div class="flexbox">
    <div>
      <h3>All Elements</h3>
      <draggable
        class="dragArea"
        :list="list1"
        :group="{ name: 'elements', put: false }"
      >
        <div class="card" v-for="(element, index) in list1" :key="index">
          {{ element.name }}
          <button v-on:click="deleteElement(index)">Delete this Item</button>
        </div>
      </draggable>
      <hr />
      <input v-model="itemData" placeholder="Add New FootBaller" />

      <button v-on:click="addItem(itemData)">Add New</button>
    </div>

    <div>
      <h3>Drop Here</h3>
      <draggable class="dragArea " :list="list2" group="elements">
        <div class="card" v-for="(element, index) in list2" :key="index">
          Name: {{ element.name }}
          <hr />
          Position of element -> {{ index + 1 }}
          <hr />
          <button v-on:click="deleteItem(index)">Delete this Item</button>
        </div>
      </draggable>
    </div>

    <div>
      <h3>Drop Here</h3>
      <draggable class="dragArea" :list="list3" group="elements">
        <div class="card" v-for="(element, index) in list3" :key="index">
          Name: {{ element.name }}
          <hr />
          Position of element -> {{ index + 1 }}
        </div>
      </draggable>
    </div>

  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  name: "Hello",
  components: {
    draggable,
  },
  methods: {
    deleteItem: function(itemId) {
      let newData = this.list2;

      newData.splice(itemId, 1);

      this.list2 = newData;
    },
    deleteElement: function(itemId) {
      let newData = this.list1;

      newData.splice(itemId, 1);

      this.list1 = newData;
    },
    addItem: function(itemData) {
      let newData = this.list1;

      newData.unshift({ name: itemData });

      this.list1 = newData;
    },
  },
  data() {
    return {
      list1: [
        { name: "Cristiano" },
        { name: "Lionel Messi" },
        { name: "Pele" },
        { name: "Dieago Maradona (RIP - LEGEND)" },
      ],
      list2: [],
      list3: [],
    };
  },
};
</script>

<style>
.flexbox {
  display: flex;
  width: 100%;
  height: 100vh;
  max-width: 768px;
  margin: auto;
}

.dragArea {
  background-color: grey;
  min-height: 500px;
  width: 250px;
  margin: 20px;
}

.flexbox .card {
  padding: 15px 25px;
  background-color: #f3f3f3;
  cursor: pointer;
  margin-bottom: 15px;
}
</style>
