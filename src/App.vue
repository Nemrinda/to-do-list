<script setup>
import { ref } from "vue";

const task = ref({
  title: "",
});
const todolist = ref([
  {
    title: "sasa",
  },
  {
    title: "kaka",
  },
]);

const search = ref("");

function AddTask() {
  if (task.value.title === "") {
    alert("Please input something.");
    return;
  }
  if (todolist.value.some((todolist) => todolist.title === task.value.title)) {
    alert("This title is already have. Please input something else.");
    return;
  }
  todolist.value.push({ ...task.value });
  task.value.title = "";
}
//====== remove by index
// function RemoveItem(index) {
//   todolist.value.splice(index, 1);
// }
function RemoveItem(title) {
  todolist.value = todolist.value.filter(
    (todolist) => todolist.title !== title,
  );
}
function Search(title) {
  todolist.value = todolist.value.filter(
    (todolist) => todolist.title === title,
  );
  search.value = "";
  console.log(title);
}

const isIcon = ref(true);
function changeMode() {
  isIcon.value = !isIcon.value;
 
}
</script>
<template>
  <div :class="isIcon ? 'bg-warning' : 'bg-success'" style="height: 100vh" class="overflow-hidden">
    <div class="p-3 text-end">
      <button @click="changeMode" class="btn btn-primary mb-4">
        <i class="bi" :class="isIcon ? 'bi-moon' : 'bi-moon-fill'"></i>
      </button>
    </div>

    <div style="height: 100vh;" class="d-flex justify-content-center align-items-center">
      <div
        class="card mb-3 "
        style="width: 500px"
      >
        <div class="card-body">
          <div
            class="header d-flex justify-content-between align-items-center mb-3"
          >
            <h5 class="card-title fw-bold" style="font-size: 30px">
              To-Do-List
            </h5>
            <button class="btn bg-primary text-light">Export to Excel</button>
          </div>
          <div class="input-group mb-3">
            <input
              type="text"
              class="form-control"
              placeholder="Add a new task"
              v-model="task.title"
            />
            <button
              class="btn bg-success text-light"
              type="button"
              id="button-addon2"
              @click="AddTask"
            >
              Add
            </button>
          </div>
          <div class="input-group mb-3">
            <input
              type="text"
              class="form-control"
              placeholder="Type to search"
              v-model="search"
            />
            <button
              class="btn bg-success text-light"
              type="button"
              id="button-addon2"
              @click="Search(search)"
            >
              Search
            </button>
          </div>
          <div
            v-for="(list, index) in todolist"
            :key="index"
            class="d-flex justify-content-between align-items-center border rounded p-2 mb-2"
          >
            <span style="font-size: 20px">{{ list.title }}</span>
            <button class="btn btn-danger" @click="RemoveItem(list.title)">
              Delete
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
