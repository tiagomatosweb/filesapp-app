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
              />
              <v-btn
                variant="tonal"
                color="primary"
                icon="mdi-download-circle"
                size="small"
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
import {ref} from 'vue';

const file = ref();

const files = [
  {
    name: 'IronMan.jpg',
    created_at: '2024-01-02 20:20:00',
  },
  {
    name: 'Icecream-sandwich.png',
    created_at: '2024-01-10 15:20:00',
  },
  {
    name: 'Wonderwoman.jpg',
    created_at: '2024-01-07 10:20:00',
  },
]
</script>
