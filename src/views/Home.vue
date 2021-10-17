<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-10">
        <h1>Заметки</h1>
        <hr><br><br>
        <button type="button" class="btn btn-success btn-sm" v-b-modal.note-modal>Добавить заметку</button>
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
    <b-modal ref="addNoteModal"
         id="note-modal"
         title="Добавте новую заметку"
         hide-footer>
  <b-form @submit="onSubmit" @reset="onReset" class="w-100">

  <b-form-group id="form-title-group"
                label="Название:"
                label-for="form-title-input">
      <b-form-input id="form-title-input"
                    type="text"
                    v-model="addNoteForm.title"
                    required
                    placeholder="Название">
      </b-form-input>
    </b-form-group>

    <b-form-group id="form-body-group"
                  label="Текст:"
                  label-for="form-body-input">
        <b-form-input id="form-body-input"
                      type="text"
                      v-model="addNoteForm.body"
                      required
                      placeholder="Введите текст заметки">
        </b-form-input>
      </b-form-group>

    <b-form-group id="form-date-group"
                label="Дата:"
                label-for="form-date-input">
       <b-form-input id="form-date-input"
                      type="date"
                      v-model="addNoteForm.createTime"
                      required
                      placeholder="Дата">
        </b-form-input>
    </b-form-group>

    <b-button type="submit" variant="primary">Сохранить</b-button>
    <b-button type="reset" variant="danger">Сбросить</b-button>
  </b-form>
</b-modal>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      notes: [],
      addNoteForm:{
        title:'',
        body:'',
        createTime:''
      },
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
    addNote(payload) {
      const path = 'http://localhost:64296/api/notes';
      axios.post(path, payload)
        .then(() => {
          console.log("POST запрос получился")
        })
        .catch((error) => {
          // eslint-отключение следующей строки
          console.log(error);
        });
    },
    initForm(){
      this.addNoteForm.title = ''
      this.addNoteForm.body = ''
      this.addNoteForm.createTime = ''

    },
    onSubmit(evt) {
      evt.preventDefault();
      this.$refs.addBookModal.hide();
      let read = false;
      if (this.addNoteForm.read[0]) read = true;
      const payload = {
        title: this.addNoteForm.title,
        body: this.addNoteForm.body,
        createTime: this.addNoteForm.createTime
      };
  },
  onReset(evt) {
      evt.preventDefault();
      this.$refs.addNameModal.hide();
      this.initForm();
    },
  
    created() {
    this.getNotes();
  },
},
};
</script>

<style>

</style>


