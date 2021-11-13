<template>
  <div class="min-h-screen flex items-center justify-center">
    <div class="w-1200 mx-auto">
      <div class="grid gap-5">
        <div class="bg-white-100 shadow-md p-10 rounded-xl border border-gray-100">
          <table class="w-full" v-if="users.length > 0">
            <thead>
              <tr class="border-b border-gray-100">
                <th class="p-4 text-sm text-left">ID</th>
                <th class="p-4 text-sm text-left">Date de création</th>
                <th class="p-4 text-sm text-left">Etat</th>
                <th class="p-4 text-sm text-left">Nom</th>
                <th class="p-4 text-sm text-left">Prénom</th>
                <th class="p-4 text-sm text-left">Nom d'utilisateur</th>
                <th class="p-4 text-sm text-left">Matricule</th>
                <th class="p-4 text-sm text-left">Actions</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(user, key) in users" :key="key">
                <td class="p-4 text-left text-sm">{{ user.id }}</td>
                <td class="p-4 text-left text-sm">{{ user.createdDate }}</td>
                <td class="p-4 text-left text-sm">
                  <template v-for="(status, index) in userStatus" :key="index">
                    <span v-if="status.name === user.status" :class="status.bgColor" class="text-white-100 py-2 px-4 rounded block text-center">{{ user.status }}</span>
                  </template>
                </td>
                <td class="p-4 text-left text-sm">{{ user.firstName }}</td>
                <td class="p-4 text-left text-sm">{{ user.lastName }}</td>
                <td class="p-4 text-left text-sm">{{ user.userName }}</td>
                <td class="p-4 text-left text-sm">{{ user.registrationNumber }}</td>
                <td class="p-4 text-left text-sm">
                  <button @click="deleteUser(key)">Detele</button>
                </td>
              </tr>
            </tbody>
          </table>
          <div v-else>
            No users
          </div>
        </div>
        <div class="bg-white-100 shadow-md p-4 rounded-xl border border-gray-100 flex items-center justify-end">
          <button class="bg-warning-100 rounded py-2 px-6 text-sm shadow-md" @click.prevent="showAddUser">Ajouter utilisateur</button>
        </div>
      </div>
    </div>
    <add-user v-if="show" @hideAddUser="hideAddUser" @addUser="addUser" />
  </div>
</template>

<script>
import AddUser from './components/AddUser'

export default {
  name: 'App',
  components: {
    AddUser
  },
  data() {
    return {
      show: false,
      users: [
        {
          id: "123456789",
          createdDate: "2021-01-06T00:00:00.000Z",
          status: "En validation",
          firstName: "Mohamed",
          lastName: "Taha",
          userName: "mtaha",
          registrationNumber: "2584",
        },
        {
          id: "987654321",
          createdDate: "2021-07-25T00:00:00.000Z",
          status: "Validé",
          firstName: "Hamid",
          lastName: "Orrich",
          userName: "horrich",
          registrationNumber: "1594",
        },
          {
          id: "852963741",
          createdDate: "2021-09-15T00:00:00.000Z",
          status: "Rejeté",
          firstName: "Rachid",
          lastName: "Mahidi",
          userName: "rmahidi",
          registrationNumber: "3576",
        }
      ],
      userStatus: [
        {
          name: 'En validation',
          bgColor: 'bg-warning-100'
        },
        {
          name: 'Validé',
          bgColor: 'bg-success-100'
        },
        {
          name: 'Rejeté',
          bgColor: 'bg-danger-100'
        }
      ]
    }
  },
  methods: {
    deleteUser(index) {
      this.users.splice(index, 1)
    },
    showAddUser() {
      this.show = true
    },
    hideAddUser() {
      this.show = false
    },
    addUser(newUser) {
      this.users.push(newUser)
      this.hideAddUser()
    }
  },
}
</script>
