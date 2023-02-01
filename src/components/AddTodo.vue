<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Todo</label>
      <input type="text" v-model="name" name="name" placeholder="Add Todo" />
    </div>
    <div class="form-control">
      <label>Description</label>
      <input
        type="text"
        v-model="description"
        name="description"
        placeholder="Add description"
      />
    </div>
    <div class="form-control">
      <label>Deadline</label>
      <input
        class="deadline"
        type="text"
        v-model="day"
        name="day"
        placeholder="DD"
      />
      /
      <input
        class="deadline"
        type="text"
        v-model="month"
        name="month"
        placeholder="MM"
      />
      /
      <input
        class="deadline"
        type="text"
        v-model="year"
        name="year"
        placeholder="YYYY"
      />
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTodo",

  data() {
    return {
      name: "",
      description: "",
      // deadline: "",
      day: "",
      month: "",
      year: "",
    };
  },

  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.name) {
        alert("Please add a name");
        return;
      }
      if (!this.description) {
        alert("Please add a description");
        return;
      }

      const deadline =
        ("00" + this.day).slice(-2) +
        "/" +
        ("00" + this.month).slice(-2) +
        "/" +
        this.year;

      if (isNaN(Date.parse(this.month + "/" + this.day + "/" + this.year))) {
        alert("Please input a valid date");
        return;
      }

      const newTodo = {
        name: this.name,
        description: this.description,
        created: new Date().toLocaleString("pt-br").slice(0, 10),
        deadline: deadline,
      };

      this.$emit("add-todo", newTodo);

      this.name = "";
      this.description = "";
      this.deadline = "";
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}

.deadline-form label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}

.form-control .deadline {
  width: 60px;
}
</style>
