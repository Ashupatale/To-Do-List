<template>
  <div class="Main-Div">
    <div>
      <h1 class="text-center text-white pt-5 pb-4">
          Welcome to your Todo List
         
      </h1>

      <div class="TodoList bg-white rounded p-5">
        <div class="d-flex">
          <!-------------Input Submit task function------------------>

          <input
            type="text"
            class="form-control text-center"
            v-model="task"
            placeholder="What you want to do Today?"
            style="width: 80%; margin-right: 5%; box-shadow: none"
          />

          <button
            type="submit"
            class="btn btn-primary submitTask p-2 d-flex"
            @click="SubmitClick()"
          >
            <i class="fab fa-telegram-plane fa-lg"></i>
            <span>Submit</span>
          </button>
        </div>
        <span class="text-danger">{{ ErrorMsg }}</span>

        <div class="List-Table mt-5" v-if="taskList.length > 0">
          <table class="table">
            <thead class="thead-dark">
              <tr>
                <th scope="col" class="text-start">Task</th>
                <th scope="col">Status</th>
                <th scope="col" class="text-center">Edit</th>
                <th scope="col" class="text-center">Delete</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(list, index) in taskList" :key="list.id">
                <td class="text-start" :class="{ strike: list.status }">
                  {{ list.name }}
                </td>
                <td>{{ list.status }}</td>
                <!-------------Edit task function------------------>
                <td class="text-center" @click="editTask(index)">
                  <abbr title="Edit Task"
                    ><span class="fa fa-pen spanBtn text-success"></span
                  ></abbr>
                </td>
                <!-------------Delete task function------------------>

                <td class="text-center" @click="deleteTask(index)">
                  <abbr title="Delete Task?"
                    ><span class="fa fa-trash spanBtn text-danger"></span
                  ></abbr>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div v-else class="text-center fw-bold mt-3">
          <p>You have no Todo task left! Lets Create now!</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      isActive: true,
      ErrorMsg: "",
      task: "",
      editTaskList: null,
      taskList: [
        {
          name: "Wake up at 6AM",
          status: false,
        },
        {
          name: "Go for Gym at 7AM",
          status: false,
        },
        {
          name: "Take a shower at 9AM ",
          status: false,
        },
      ],
    };
  },

  methods: {
    SubmitClick() {
      if (this.task.length === 0) return;

      if (this.editTaskList === null) {
        this.taskList.push({
          name: this.task,
          status: false,
        });
      } else {
        this.taskList[this.editTaskList].name = this.task;
      }

      this.task = "";
    },

    deleteTask(index) {
      this.taskList[index].status = true;

      setTimeout(() => {
        this.taskList.splice(index, 1);
      }, 1000);
      console.log("index", index);
    },

    editTask(index) {
      this.task = this.taskList[index].name;
      this.editTaskList = index;
    },
  },
};
</script>

<style>
.Main-Div {
  background: #ee0979;
  background: -webkit-linear-gradient(to right, #ff6a00, #ee0979);
  background: linear-gradient(to right, #ff6a00, #ee0979);
  height: 100vh;
}
.TodoList {
  width: 50%;
  margin: auto;
  height: auto;
}
.spanBtn {
  cursor: pointer;
}
.submitTask {
  width: 18%;
  justify-content: space-around;
}
.strike {
  text-decoration: line-through;
  color: red;
}
</style>
