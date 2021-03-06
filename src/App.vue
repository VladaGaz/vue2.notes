<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1 v-show="showNotes">{{ title }}</h1>
          <newNote v-show="showNotes" :note="note" @addNote="addNote" />
          <message v-if="message" :message="message" />
          <div v-show="showNotes" class="note-header" style="margin: 36px 0">
            <search
              :value="search"
              placeholder="Find your note"
              @search="search = $event"
            />
            <div class="icons">
              <svg
                :class="{ active: grid }"
                @click="grid = true"
                style="cursor: pointer"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                :class="{ active: !grid }"
                @click="grid = false"
                style="cursor: pointer"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>
          <notes
            :notes="notesFilter"
            :grid="grid"
            :showNotes="showNotes"
            :showIndex="showIndex"
            :showCenterNote="showCenterNote"
            @remove="removeNote"
            @change="changeNote"
            @back="backNote"
            @updateDate="updateDate"
            @save="saveNote"
          />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message.vue";
import notes from "@/components/Notes.vue";
import newNote from "@/components/NewNote.vue";
import search from "@/components/Search.vue";

export default {
  components: {
    message,
    notes,
    newNote,
    search,
  },
  data() {
    return {
      title: "NotesApp",
      search: "",
      message: null,
      priority: "standard",
      grid: true,
      showNotes: true,
      showIndex: -1,
      showCenterNote: false,
      note: {
        title: "",
        descr: "",
        priority: "standard",
      },
      notes: [
        {
          title: "First Note",
          descr: "Description for first note",
          priority: "standard",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Second Note",
          descr: "Description for second note",
          priority: "important",
          date: new Date(Date.now()).toLocaleString(),
        },
        {
          title: "Third Note",
          descr: "Description for third note",
          priority: "veryImportant",
          date: new Date(Date.now()).toLocaleString(),
        },
      ],
    };
  },
  computed: {
    notesFilter() {
      let array = this.notes;
      let search = this.search;

      if (!search) {
        return array;
      }
      search = search.trim().toLowerCase();

      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      return array;
    },
  },
  methods: {
    addNote() {
      let { title, descr, priority } = this.note;

      if (title === "") {
        this.message = "Title can not be blank!";
        return false;
      }
      this.notes.push({
        title,
        descr,
        priority,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.message = null;
      this.note.title = "";
      this.note.descr = "";
      this.note.priority = "standard";
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
    changeNote(index) {
      this.showNotes = false;
      this.showIndex = index;
      //для добавления отцентрирования кнопки
      this.showCenterNote = true;
    },
    backNote() {
      this.showNotes = true;
    },
    updateDate({ index, data }) {
      this.notes[index].date = data;
    },
    saveNote(noteObj) {
      if (noteObj.newNote.title !== "") {
        this.notes[noteObj.index].title = noteObj.newNote.title;
      }
      if (noteObj.newNote.descr !== "") {
        this.notes[noteObj.index].descr = noteObj.newNote.descr;
      }
      this.showNotes = true;
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  color: royalblue;
  margin-top: 0px;
}
section {
  position: relative;
  padding: 40px 0;
}
.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0 auto;
}

.container {
  width: 100%;
  flex: 0 0 auto;
  position: relative;
  margin: 0 auto;
}
</style>
