<template>
  <div class="notes">
    <div
      class="note"
      :class="{ full: !grid }"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header" :class="{ full: !grid }">
        <p>{{ note.title }}</p>
        <p style="cursor: pointer" @click="removeNote(index)">
          <img src="../assets/close.png" />
        </p>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      this.$emit("remove", index);
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
.note-body > p {
  margin: 20px 0;
}
.note-body > span {
  font-size: 14px;
  color: #999;
}
</style>