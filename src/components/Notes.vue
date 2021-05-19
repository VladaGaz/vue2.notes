<template>
  <div class="notes">
    <div
      class="note"
      :class="{
        full: !grid,
        center: showCenterNote,
        important: note.priority === 'important',
        'very-important': note.priority === 'veryImportant',
      }"
      v-show="showIndex === index || showNotes"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header" :class="{ full: !grid }">
        <p v-if="showNotes">{{ note.title }}</p>
        <input
          v-else
          v-model="note.title"
          :class="{
            standard: note.priority === 'standard',
            important: note.priority === 'important',
            'very-important': note.priority === 'veryImportant',
          }"
        />
        <div class="icon-img">
          <p
            style="cursor: pointer"
            @click="changeNote(index)"
            v-show="showNotes"
          >
            <img src="../assets/change.png" style="width: 15px" />
          </p>
          <p
            style="cursor: pointer"
            @click="
              backNote(index),
                updateDate(index, new Date(Date.now()).toLocaleString())
            "
            v-show="!showNotes"
          >
            <img src="../assets/back.png" style="width: 15px" />
          </p>
          <p
            style="cursor: pointer"
            @click="removeNote(index)"
            v-show="showNotes"
          >
            <img src="../assets/close.png" style="width: 13px" />
          </p>
        </div>
      </div>
      <div class="note-body">
        <p v-if="showNotes">{{ note.descr }}</p>
        <input
          v-else
          v-model="note.descr"
          :class="{
            standard: note.priority === 'standard',
            important: note.priority === 'important',
            'very-important': note.priority === 'veryImportant',
          }"
        />
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      placeholder: "",
    };
  },
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
    showNotes: {
      type: Boolean,
      required: true,
    },
    showIndex: {
      type: Number,
      required: true,
    },
    showCenterNote: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      this.$emit("remove", index);
    },
    changeNote(index) {
      this.$emit("change", index);
    },
    backNote() {
      this.$emit("back");
    },
    updateDate(index, data) {
      this.$emit("updateDate", { index, data });
    },
  },
};
</script>

<style>
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 46%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: aliceblue;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.02);
}
.full {
  width: 100%;
  text-align: center;
  justify-content: center;
}
.center {
  margin: auto;
}
.note:hover {
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
  transform: translate(0, -6px);
  transition-delay: 0s !important;
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.note-header > h1 {
  font-size: 32px;
}
.note-header > p {
  font-size: 22px;
  color: royalblue;
}
.note-header > input {
  margin: 22px 0;
  font-size: 22px;
  color: royalblue;
  border: none;
  outline: none;
}
.note-header > p > img {
  width: 10px;
}
.icons > svg {
  margin-right: 12px;
  color: #999;
}
.icons > svg.active {
  color: royalblue;
}
.icons > svg:last-child {
  margin-right: 0;
}
.icon-img {
  display: flex;
}
.icon-img > p {
  margin-left: 10px;
}
.note-body > p {
  margin: 20px 0;
}
.note-body > input {
  margin: 20px 0;
  border: none;
  outline: none;
  width: 100%;
}
.note-body > span {
  font-size: 14px;
  color: #999;
}
.important {
  background-color: rgb(255, 254, 174);
}
.very-important {
  background-color: #ffb1ab;
}
.standard {
  background-color: aliceblue;
}
</style>