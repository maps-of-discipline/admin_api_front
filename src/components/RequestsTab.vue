<template>
  <!-- Toast -->
  <v-snackbar v-model="snackbar" :color="snackbarColor" timeout="3000" location="left" multi-line>
    {{ snackbarMessage }}
    <template #actions>
      <v-progress-linear color="black" height="2" absolute bottom />
    </template>
  </v-snackbar>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { getServiceUsers } from '../services/user';
import { useToast } from "../composable/useToast";
import type { Service } from '../interfaces/service';

export default defineComponent({
  name: 'RequestsTab',
  props: {
    service: {
      type: Object as () => Service,
      required: true,
    },
    search: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      requests: [],
      loading: false,
      headers: [
        { title: 'ФИО', value: 'fio' },
        { title: 'Логин', value: 'login' },
        { title: 'Почта', value: 'email' },
        { title: 'Роль', value: 'role' },
      ],
      ...useToast(),
    };
  },
  //   watch: {
  //     'service': {
  //       handler: 'getServiceUsersData',
  //       immediate: true,
  //     },
  //   },
  //   methods: {
  //     async getServiceUsersData() {
  //       if (!this.service.name) {
  //         return;
  //       }
  //       try {
  //         const response = await getServiceUsers({ id: "", name: this.service.name, verbose_name: "" });
  //         if (response.success) {
  //           this.users = (response.data as User[]).map((user) => ({
  //             id: user.id,
  //             name: user.name,
  //             surname: user.surname,
  //             patronymic: user.patronymic,
  //             login: user.login,
  //             email: user.email,
  //             role: user.role,
  //           }));
  //         } else {
  //           this.showToast(response.error || "Ошибка получения данных.", "error");
  //         }
  //       } catch (error) {
  //         this.showToast("Ошибка при запросе.", "error");
  //       }
  //     },
  //   },
});
</script>
