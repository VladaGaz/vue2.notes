<template>
  <div class="new-note">
    <label>Title</label>
    <input v-model="note.title" type="text" />
    <label>Description</label>
    <textarea v-model="note.descr"></textarea>
    <taskPriority :dataSelect="note.priority" @onChange="priorityMethods" />
    <button class="btn" @click="addNote">New note</button>
  </div>
</template>

<script>
import taskPriority from "@/components/TaskPriority.vue";
export default {
  components: {
    taskPriority,
  },
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note);
    },
    priorityMethods(objectPriority) {
      this.note.priority = objectPriority.select;
    },
  },
};
</script>

<style  scoped>
.new-note {
  text-align: center;
}
textarea {
  resize: none;
  overflow: auto;
  vertical-align: top;
  box-shadow: none;
  -webkit-box-shadow: none;
  -moz-box-shadow: none;
}
input,
textarea,
button {
  outline: none;
  border: none;
  font-size: 100%;
  margin: 0;
  border: 1px solid #909399;
}
button,
input {
  line-height: normal;
}
label {
  display: block;
  font-size: 23px;
  margin-bottom: 10px;
  text-align: center;
}
input {
  padding: 16px 26px;
  margin-bottom: 30px;
  border-radius: 20px;
}
textarea {
  padding: 30px 27px;
  border-radius: 14px;
}
input,
textarea {
  width: 50%;
}
.btn {
  padding: 0.8em 2.6em;
  line-height: 1;
  text-transform: uppercase;
  cursor: pointer;
  border-radius: 30px;
  color: #ffffff;
  border: 1px solid #494ce8;
  background-color: #494ce8;
  display: block;
  margin: 0px auto;
  margin-top: 30px;
}
</style>