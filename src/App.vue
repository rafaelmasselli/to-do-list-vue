<template>
  <div id="app">
    <NavBarVue />
    <h1 class="title__home">TodoList</h1>
    <div class="box container">
      <NewList @taskAdded="addTask" />
    </div>
    <hr class="line" />
    <div class="container__progress">
      <ProgressListVue :progress="progress" v-if="progress > 0" />
    </div>
    <div class="cards container">
      <Card
        v-for="list in lists"
        v-bind:key="list.id"
        :id="list.id"
        :title="list.title"
        :description="list.description"
        :pending="list.pending"
        @taskConcluded="concludedTask"
        @taskDelete="deleteTask"
        @taskReset="concludedTask"
      />
    </div>
  </div>
</template>

<script>
import Card from "@/components/CardList";
import NewList from "@/components/NewList";
import ProgressListVue from "./components/ProgressList";
import NavBarVue from "./components/shared/NavBar";

export default {
  name: "App",
  components: {
    NavBarVue,
    Card,
    NewList,
    ProgressListVue,
  },
  data() {
    return {
      lists: [],
    };
  },
  methods: {
    addTask(task) {
      this.lists.push({
        id: task.id,
        title: task.title,
        description: task.description,
        pending: false,
      });
    },

    concludedTask(task) {
      this.lists.map((res, index) => {
        if (task.id == res.id) {
          this.lists[index].pending
            ? (this.lists[index].pending = false)
            : (this.lists[index].pending = true);
        }
      });
    },
    deleteTask(task) {
      this.lists.map((res, index) => {
        if (task.id == res.id) {
          this.lists.splice(index, 1);
        }
      });
    },
  },
  computed: {
    progress() {
      const total = this.lists.length;
      const done = this.lists.filter((t) => t.pending).length;
      return Math.round((done / total) * 100) || 0;
    },
  },
  watch: {
    lists: {
      deep: true,
      handler() {
        window.localStorage.setItem("task", JSON.stringify(this.lists));
      },
    },
  },
  created() {
    const json = window.localStorage.getItem("lists");
    const array = JSON.parse(json);
    this.lists = Array.isArray(array) ? array : [];
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  background: #e2efde;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.title__home {
  margin: 25px 0;
  font-size: 50px;
}

.container__progress {
  width: 100%;
  display: flex;
  justify-content: center;
  align-content: center;
}
.progressNul {
  margin: 30px 0 -20px 0;
}

.box {
  flex-direction: column;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.cards {
  overflow: auto;
  flex-wrap: wrap;
}

.line {
  margin: 40px 0;
  height: 10px;
}
</style>
