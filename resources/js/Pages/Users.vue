<template>
    <app-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Users
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                      <div class="md:container md:mx-auto py-12">
    <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
      <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg px-4 py-4">
        <div class="bg-teal-100 border-t-4 border-teal-500 rounded-b text-teal-900 px-4 py-3 shadow-md my-3" role="alert" v-if="$page.flash.message">
          <div class="flex">
            <div>
              <p class="text-sm">{{ $page.flash.message }}</p>
            </div>
          </div>
        </div>
        <button @click="openModal()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded my-3">Create New Post</button>
        <table class="table-auto w-full text-center">
          <thead>
            <tr class="bg-gray-100">
              <th class="px-4 py-2">Photo</th>
              <th class="px-4 py-2">Prefix Name</th>
              <th class="px-4 py-2">First Name</th>
              <th class="px-4 py-2">Middle Name</th>
              <th class="px-4 py-2">Last Name</th>
              <th class="px-4 py-2">Suffix Name</th>
              <th class="px-4 py-2">Username</th>
              <th class="px-4 py-2">Email</th>
              <th class="px-4 py-2">Type</th>
              <th class="px-4 py-2">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="user in users" :key="user.id">
              <td> Photo</td>
              <td>{{ user.prefixname }}</td>
              <td>{{ user.firstname  }}</td>
              <td>{{ user.middlename }}</td>
              <td>{{ user.lastname }}</td>
              <td>{{ user.suffixname }}</td>
              <td>{{ user.username }}</td>
              <td>{{ user.email }}</td>
              <td>{{ user.type }}</td>
              <td width="130">
                <button @click="edit(user)" class="bg-green-500 hover:bg-green-700 text-white font-light py-1 px-1 rounded">View</button>
                <button wire:click="" class="bg-red-500 hover:bg-red-700 text-white font-light py-1 px-1 rounded">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>
        <div class="fixed z-10 inset-0 overflow-y-auto ease-out duration-400" v-if="isOpen">
          <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <div class="fixed inset-0 transition-opacity">
              <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
            </div>
            <!-- This element is to trick the browser into centering the modal contents. -->
            <span class="hidden sm:inline-block sm:align-middle sm:h-screen"></span>​
            <div class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full" role="dialog" aria-modal="true" aria-labelledby="modal-headline">
              <form>
                <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                  <div class="">

                    <div class="mb-4">
                      <label for="exampleFormControlInput1" class="block text-gray-700 text-sm font-bold mb-2">Photo:</label>
                      <input type="text" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput1" placeholder="Enter Title" v-model="form.photo" />
                      <div v-if="$page.errors.title" class="text-red-500">{{ $page.errors.title[0] }}</div>
                    </div>


                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">Prefix Name:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.prefixname" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">First Name:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.firstname" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                    
                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">Middle Name:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.middlename" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">Last Name:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.lastname" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">Suffix Name:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.suffixname" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">Username:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.username" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">Email:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.email" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                    
                    <div class="mb-4">
                      <label for="exampleFormControlInput2" class="block text-gray-700 text-sm font-bold mb-2">Type:</label>
                      <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="exampleFormControlInput2" v-model="form.type" placeholder="Enter Body"></textarea>
                      <div v-if="$page.errors.body" class="text-red-500">{{ $page.errors.body[0] }}</div>
                    </div>

                  </div>
                </div>
                <div class="bg-gray-50 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
                  <span class="flex w-full rounded-md shadow-sm sm:ml-3 sm:w-auto">
                    <button
                      wire:click.prevent="store()"
                      type="button"
                      class="inline-flex justify-center w-full rounded-md border border-transparent px-4 py-2 bg-green-600 text-base leading-6 font-medium text-white shadow-sm hover:bg-green-500 focus:outline-none focus:border-green-700 focus:shadow-outline-green transition ease-in-out duration-150 sm:text-sm sm:leading-5"
                      v-show="!editMode"
                      @click="save(form)"
                    >
                      Save
                    </button>
                  </span>
                  <span class="flex w-full rounded-md shadow-sm sm:ml-3 sm:w-auto">
                    <button
                      wire:click.prevent="store()"
                      type="button"
                      class="inline-flex justify-center w-full rounded-md border border-transparent px-4 py-2 bg-green-600 text-base leading-6 font-medium text-white shadow-sm hover:bg-green-500 focus:outline-none focus:border-green-700 focus:shadow-outline-green transition ease-in-out duration-150 sm:text-sm sm:leading-5"
                      v-show="editMode"
                      @click="update(form)"
                    >
                      Update
                    </button>
                  </span>
                  <span class="mt-3 flex w-full rounded-md shadow-sm sm:mt-0 sm:w-auto">
                    <button
                      @click="closeModal()"
                      type="button"
                      class="inline-flex justify-center w-full rounded-md border border-gray-300 px-4 py-2 bg-white text-base leading-6 font-medium text-gray-700 shadow-sm hover:text-gray-500 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue transition ease-in-out duration-150 sm:text-sm sm:leading-5"
                    >
                      Cancel
                    </button>
                  </span>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout'
    import Users from '@/Pages/Users'

    export default {
        props: {
          users : Array
        },
        components: {
            AppLayout,
            Users,
        },
        data() {
            return {
                editMode: false,
                isOpen: false,
                form: {
                    title: null,
                    body: null,
                },
            };
        },
        methods: {
            openModal: function () {
                this.isOpen = true;
            },
            closeModal: function () {
                this.isOpen = false;
                this.reset();
                this.editMode=false;
            },
            edit: function (data) {
                  this.$inertia.visit('user/'+data.id);
            },
        }
    }
</script>
