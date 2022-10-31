<template>
  <div class="box__inputs">
    <h2 class="box__title">Adicionar tarefa</h2>
    <div class="box__input">
      <label class="label__title">Titulo</label>
      <input v-model="title" class="input__card title" type="text" />
    </div>
    <div class="box__input">
      <label class="label__description">Descrição</label>
      <textarea
        v-model="description"
        class="input__card description"
        type="text"
      />
    </div>
    <button v-on:click="Add" class="btn">Adicionar</button>
  </div>
</template>

<script>
import { uuid } from "vue-uuid";

export default {
  data() {
    return {
      description: "",
      title: "",
    };
  },

  methods: {
    Add() {
      if (this.title === "") {
        alert("O campo titulo não pode estar vazia");
      } else {
        if (this.description === "") {
          this.description = "Sem descrição";
        }
        this.$emit("taskAdded", {
          id: uuid.v4(),
          title: this.title,
          description: this.description,
        });
        this.title = "";
        this.description = "";
      }
    },
  },
};
</script>

<style>
.box__input {
  flex-direction: column;
  display: flex;
  align-items: center;
}

.box__inputs {
  width: 360px;
  height: 365px;
  background: #ffffff;
  border-radius: 5px;
  box-shadow: 10px 10px 20px 1px rgba(0, 0, 0, 0.5);
}

.input__card {
  width: 90%;
  font-size: 20px;
  border-radius: 5px;
  background: white;
  text-align: center;
}

.btn {
  margin-top: 25px;
  width: 100%;
  height: 40px;
  font-size: 20px;
  border: 0px;
  color: white;
  background-color: black;
  cursor: pointer;

  transition: 2s;
}
.btn:hover {
  color: black;
  background-color: white;
  border: 1px solid black;

  transition: 1s;
}

.box__title {
  margin: 20px 0 0px 0;
}

.title {
  height: 40px;
}

.description {
  height: 100px;
}

.label__description,
.label__title {
  font-size: 20px;
  margin-top: 15px;
}
</style>
