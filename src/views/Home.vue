<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-10">
        <h1>Заметки</h1>
        <hr><br><br>
        <button type="button" class="btn btn-success btn-sm">Добавить заметку</button>
        <br><br>
        <table class="table table-hover">
          <thead>
            <tr>
              <th scope="col">Название</th>
              <th scope="col">Заметка</th>
              <th scope="col">Дата создания</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
             <tr v-for="(note, index) in notes" :key="index">
              <td>{{note.name}}</td>
              <td>{{note.body}} </td>
              <td>{{note.createTime}}</td>
              <td>
                <button type="button" class="btn btn-warning btn-sm">Изменить</button>
                <button type="button" class="btn btn-danger btn-sm">Удалить</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      notes: [],
    };
  },
  methods: {
    getNotes() {
      const path = 'http://localhost:64296/api/notes';
      axios.get(path)
        .then((res) => {
          this.notes = res.data;
        })
        .catch((error) => {
          // eslint-отключение следующей строки
          console.error(error);
        });
    },
  },
    created() {
    this.getNotes();
  },
};
</script>

<style>

</style>


