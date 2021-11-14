<template>
  <div class="fixed inset-0 flex items-center justify-center">
    <div class="bg-white-100 p-10 rounded-xl z-10 w-1200">
      <div class="flex items-center justify-between mb-5">
        <h1 class="font-semibold text-2xl">Ajout d'utilisateurs</h1>
      </div>
      <div class="grid gap-y-5">
        <div class="grid grid-cols-3 gap-y-5 gap-x-20">
          <div class="form-group">
            <label for="nom" class="block mb-2 text-base">Nom</label>
            <input id="nom" class="border border-gray-100 rounded w-full h-10 px-4 outline-none focus:outline-none" v-model="form.lastName" />
          </div>
          <div class="form-group">
            <label for="prenom" class="block mb-2 text-base">Prénom</label>
            <input id="prenom" class="border border-gray-100 rounded w-full h-10 px-4 outline-none focus:outline-none" v-model="form.firstName" />
          </div>
          <div class="form-group">
            <label for="etat" class="block mb-2 text-base">Etat</label>
            <select id="etat" v-model="form.status" class="border border-gray-100 rounded w-full h-10 px-4 outline-none focus:outline-none">
              <option value="En validation" selected>En validation</option>
              <option value="Validé">Validé</option>
              <option value="Rejeté">Rejeté</option>
            </select>
          </div>
          <div class="form-group">
            <label for="username" class="block mb-2 text-base">Nom d'utilisateur</label>
            <input id="username" class="border border-gray-100 rounded w-full h-10 px-4 outline-none focus:outline-none" v-model="form.userName" />
          </div>
          <div class="form-group">
            <label for="created-date" class="block mb-2 text-base">Date de création</label>
            <input id="created-date" class="border border-gray-100 rounded w-full h-10 px-4 outline-none focus:outline-none" v-model="form.createdDate" />
          </div>
        </div>
        <div class="grid grid-cols-3 gap-x-20">
          <div class="form-group">
            <label for="matricule" class="block mb-2 text-base">Matricule</label>
            <input id="matricule" class="border border-gray-100 rounded w-full h-10 px-4 outline-none focus:outline-none" v-model="form.registrationNumber" />
          </div>
        </div>
      </div>
      <div class="mt-5 flex items-center justify-end">
        <button class="bg-warning-100 rounded py-2 px-10 text-sm h-10 shadow-md" @click.prevent="addUser">
          Enregistrer
        </button>
      </div>
    </div>
    <div class="fixed inset-0 bg-overlay-100 cursor-pointer" @click="hideAddUser" />
  </div>
</template>

<script>
var today = new Date();
var date = today.getDate()+'/'+(today.getMonth()+1)+'/'+today.getFullYear();
export default {
  emits: ['hideAddUser', 'addUser'],

  data() {
    return {
      form: {
        id: Math.floor(Math.random() * 1000000000),
        createdDate: date,
        status: '',
        firstName: '',
        lastName: '',
        userName: '',
        registrationNumber: ''
      }
    }
  },
  methods: {
    hideAddUser() {
      this.$emit('hideAddUser', false)
    },
    addUser() {
      this.$emit('addUser', this.form)
    }
  },
}
</script>