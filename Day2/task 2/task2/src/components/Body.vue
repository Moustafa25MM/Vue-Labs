<template>
  <div>
    <table class="table table-striped table-bordered">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="student in students" :key="student.id">
          <td>{{ student.id }}</td>
          <td>{{ student.name }}</td>
          <td>{{ student.city }}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <th colspan="3"># Of students: {{ students.length }}</th>
        </tr>
      </tfoot>
    </table>
    <button class="btn btn-primary" @click="showModal = true"> Add New Student </button>

    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <h2>Add New Student</h2>
        <div class="form-group">
          <label for="name">Name:</label>
          <input type="text" id="name" v-model="newStudent.name" class="form-control">
        </div>
        <div class="form-group">
          <label for="city">City:</label>
          <input type="text" id="city" v-model="newStudent.city" class="form-control">
        </div>
        <div class="modal-buttons">
          <button class="btn btn-primary" @click="addStudent">Add</button>
          <button class="btn btn-secondary" @click="closeModal">Cancel</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import students from "../students";

export default {
  data: () => ({
    students: students,
    showModal: false,
    newStudent: { 
      id: Math.max(...students.map(s => s.id)) + 100,
       name: "", 
       city: "" 
      }
  }),
  methods: {
    addStudent() {
      this.students.push(this.newStudent);
      this.newStudent = { id: this.newStudent.id + 1, 
        name: "", 
        city: "" };
      this.showModal = false;
    },
    closeModal() {
      this.showModal = false;
    }
  }
};
</script>

<style>
.modal {
  position: fixed;
  top: 50;
  left: 50;
  width: 50%;
  height: 50%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 2;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
}

.modal-buttons {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
}
</style>