<template>
  <v-app class="pa-10">
    <v-main>
      <v-container>
        <div class="d-flex justify-end">
          <div class="w-50">
          <v-file-input
            v-model="file"
            variant="solo-filled"
          />
          </div>
        </div>

        <v-table>
          <thead>
          <tr>
            <th class="text-left">
              Nome
            </th>
            <th class="text-left">
              Criado em
            </th>
            <th class="text-right">
              Ação
            </th>
          </tr>
          </thead>
          <tbody>
          <tr
            v-for="item in files"
            :key="item.name"
          >
            <td>{{ item.name }}</td>
            <td>{{ item.created_at }}</td>
            <td class="text-right">
              <v-btn
                variant="tonal"
                color="red"
                icon="mdi-trash-can-outline"
                size="small"
                class="mr-2"
                @click="deleteFile(item.id)"
              />
              <v-btn
                variant="tonal"
                color="primary"
                icon="mdi-download-circle"
                size="small"
                @click="downloadFile(item.name, item.id)"
              />
            </td>
          </tr>
          </tbody>
        </v-table>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import {ref, watch} from 'vue';
import axios from 'axios';
import fileDownload from 'js-file-download';

const file = ref([]);
watch(file, (vl) => {
  uploadFile(vl[0])
})

const files = ref([])
function getFiles() {
  axios
    .get('http://localhost:8000/api/files')
    .then((response) => {
      files.value = response.data.data
    })
}
getFiles()

function deleteFile(id) {
  axios
    .delete(`http://localhost:8000/api/files/${id}`)
    .then(() => {
      getFiles()
    })
}

function uploadFile(file) {
  axios
    .postForm('http://localhost:8000/api/files',
      {
        file
      }
    )
    .then((response) => {
      files.value.push(response.data.data)
      file.value = []
    })
}

function downloadFile(name, id) {
  axios
    .get(`http://localhost:8000/api/files/${id}`, {
      responseType: 'blob',
    })
    .then((response) => {
      fileDownload(response.data, name)
    })
}
</script>
