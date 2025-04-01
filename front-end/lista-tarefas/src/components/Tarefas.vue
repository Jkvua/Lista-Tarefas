<template>
    <div class="container">
      <div class="title">
        <h1>Lista de Tarefas</h1>
      </div>
      <div class="form">
        <input 
          type="text" 
          placeholder="Nova tarefa" 
          v-model="newTask" 
          @keyup.enter="addTask" 
        />
        <button @click="addTask">+<i class="fas fa-plus"></i></button>
      </div>
      <div class="task-box">
        <ul class="task-list">
          <li v-for="task in tasks" :key="task.id">
            <span class="task-item" @click="toggleTaskCompletion(task)">
              <span class="task-checkbox" :class="{'completed': task.completed}"></span>
              {{ task.title }}
            </span>
            <button class="delete-btn" @click="deleteTask(task.id)">
              <i class="far fa-trash-alt"></i>
            </button>
          </li>
        </ul>
      </div>
      <div class="clearBtns">
        <button @click="clearCompleted">Limpar completas</button>
        <button @click="clearAll">Limpar tudo</button>
      </div>
      <div class="pendingTasks">
        <span>Tarefas pendentes: {{ pendingTasks }}</span>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Tarefas',
    data() {
      return {
        tasks: [
          { id: 1, title: "Aniversário", completed: false },
          { id: 2, title: "Assistir Netflix", completed: false }
        ],
        newTask: '',
      };
    },
    computed: {
      pendingTasks() {
        return this.tasks.filter(task => !task.completed).length;
      },
    },
    methods: {
      addTask() {
        if (this.newTask.trim()) {
          this.tasks.push({
            id: Date.now(),
            title: this.newTask,
            completed: false,
          });
          this.newTask = "";
        }
      },
      toggleTaskCompletion(task) {
        task.completed = !task.completed;
      },
      deleteTask(taskId) {
        this.tasks = this.tasks.filter(task => task.id !== taskId);
      },
      deleteTask(taskId) {
        this.tasks = this.tasks.filter(task => task.id !== taskId);
      },
      clearCompleted() {
        this.tasks = this.tasks.filter(task => !task.completed);
      },
      clearAll() {
        this.tasks = [];
      },
    },
  };
  </script>
  
  <style>
  body {
    background-image: linear-gradient(#84c1dd, #b6e0eb, #70b6df);
    /* background-color: #3b8ddf; */
    font-family: Arial, sans-serif;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  .container {
    width: 100%;
    max-width: 400px;
    text-align: center;
    border: 2px solid #ddd;
    border-radius: 20px;
    padding: 20px;
    background: rgb(255, 255, 255);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  .title h1 {
    color: #333;
  }
  .form {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
  }
  .form input {
    flex: 1;
    padding: 10px;
    border: 2px solid #ddd;
  }
  /* Tarefas.vue */
  .form button {
    background: none; /* Removendo o fundo */
    border: none; /* Removendo a borda */
    font-size: 30px;  /* Tamanho do símbolo + */
    color: #007bffc0;  /* Cor do símbolo */
    cursor: pointer;
    padding: 0;  /* Removendo o padding */
    display: inline-flex;
    justify-content: center;
    align-items: center;
  }
  
  .task-box {
    padding: 10px;
    background: white;
  }
  .task-list {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  .task-list li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px;
    border-bottom: 1px solid #ddd;
    transition: opacity 0.3s;
  }
  .task-item {
    display: flex;
    align-items: center;
    gap: 10px;
    cursor: pointer;
  }
  .task-checkbox {
    width: 15px;
    height: 15px;
    border: 2px solid #007bff;
    border-radius: 50%;
    display: inline-block;
    transition: background 0.3s;
  }
  .task-checkbox.completed {
    background: #007bff;
  }
  .delete-btn {
    background: none;
    border: none;
    cursor: pointer;
    color: #007bff;
  }
  .clearBtns button {
    margin-top: 10px;
    padding: 10px;
    border: none;
    background: #007bffbe;
    color: white;
    cursor: pointer;
    border-radius: 20px;
  }
  .pendingTasks {
    margin-top: 10px;
    font-size: 16px;
    color: #555;
  }
  
  
  </style>