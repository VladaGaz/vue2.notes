<template>
  <div class="task-priority">
    <p>Task priority</p>
    <select size="1" v-model="select" @change="onChange()">
      <option disabled>Select task priority</option>
      <option value="standard">standard</option>
      <option value="important">important</option>
      <option value="veryImportant">very important</option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    dataSelect: {
      type: String,
      default: "standard",
    },
  },
  data() {
    return {
      select: this.dataSelect,
    };
  },
  methods: {
    onChange() {
      this.$emit("onChange", { select: this.select });
    },
  },
  watch: {
    dataSelect: function (value) {
      this.select = value;
    },
  },
};
</script>


<style  scoped>
.task-priority {
  text-align: center;
}
p {
  display: block;
  font-size: 23px;
  margin-bottom: 10px;
  text-align: center;
}
select {
  width: 50%;
  font-size: 15px;
  text-align-last: center;
}
</style>