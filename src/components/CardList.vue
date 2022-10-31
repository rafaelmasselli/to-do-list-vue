<template>
  <div class="card__list" v-bind:class="{ danger: pending }">
    <div v-if="pending" class="container__tag">
      <div class="tag come__back" v-on:click="reset"></div>
      <div class="tag go__out" v-on:click="del"></div>
    </div>
    <div v-if="!pending" class="container__tag">
      <div class="tag"></div>
      <div class="tag check" v-on:click="concluded"></div>
    </div>
    <div class="card__container">
      <h1 class="title__list text" v-bind:class="{ danger__text: pending }">
        {{ title }}
      </h1>
      <h5 class="description text" v-bind:class="{ danger__text: pending }">
        {{ description }}
      </h5>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
    },
    title: {
      type: String,
      default: "Sem titulo",
    },
    description: {
      type: String,
      default: "Sem descrição",
    },
    pending: {
      type: Boolean,
      required: true,
    },
  },

  methods: {
    reset() {
      this.$emit("taskReset", {
        id: this.id,
      });
    },
    concluded() {
      this.$emit("taskConcluded", {
        id: this.id,
      });
    },
    del() {
      this.$emit("taskDelete", {
        id: this.id,
      });
    },
  },
};
</script>

<style>
.card__list {
  width: 300px;
  height: 200px;
  margin: 20px;
  background: #808f87;
  color: white;
  box-shadow: 1px 10px 10px 2px rgba(0, 0, 0, 0.2);
}
.card__container {
  align-content: center;
  flex-direction: column;

  word-wrap: break-word;
}
.container__tag {
  display: flex;
  justify-content: space-between;

  margin: 10px 20px -30px 20px;
}

.title__list,
.description {
  overflow: auto;
}

.title__list {
  font-size: 20px;
  margin: 30px 0 15px 0;
}
.description {
  margin: 0 20px;
}

.danger {
  background-color: rgb(161, 245, 165);
}

.danger__text {
  text-decoration: line-through;
}

.tag {
  width: 10px;
  cursor: pointer;
}

.go__out:after {
  content: "\274c";
}

.come__back:after {
  content: "\21BB";
  font-size: 25px;
  margin: 0 -10px;
}

.check:after {
  font-size: 25px;
  content: "\2713";
  color: rgb(161, 245, 165);
  margin: 0 -10px;
}
</style>
