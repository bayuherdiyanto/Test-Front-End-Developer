<template>
        <Transition name="slide-fade">
            <div v-if="showCreate" class="bg-white h-screen absolute top-0 right-0 w-4/12 p-5">
                <div class="flex justify-between">
                    <div>
                        Tambah Tugas Baru
                    </div>
                    <div @click="closeCreate">
                        X
                    </div>
                </div>

                <form class="space-y-6" @submit.prevent="saveCompany">
                    <div class="space-y-4 rounded-md shadow-sm">
                        <div>
                            <label for="email" class="block text-sm font-medium text-gray-700">
                                Tanggal Deadline
                            </label>
                            <div class="mt-1">
                                <input type="date" name="email" id="email"
                                    class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
                                    v-model="form.email">
                            </div>
                        </div>

                        <div>
                            <label for="name" class="block text-sm font-medium text-gray-700">
                                Kategori Warna Tugas
                            </label>
                            <div class="mt-1">
                                <input type="color" name="name" id="name"
                                    class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
                                    v-model="form.name">
                            </div>
                        </div>

                        <div>
                            <label for="address" class="block text-sm font-medium text-gray-700">Address</label>
                            <div class="mt-1">
                                <textarea v-model="form.address" class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"></textarea>
                                
                            </div>
                        </div>

                        <div>
                            <label for="website" class="block text-sm font-medium text-gray-700">Website</label>
                            <div class="mt-1">
                                <input type="text" name="website" id="website"
                                    class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
                                    v-model="form.website">
                            </div>
                        </div>
                    </div>

                    <button type="submit"
                            class="inline-flex items-center px-4 py-2 text-xs font-semibold tracking-widest text-white uppercase bg-gray-800 rounded-md border border-transparent ring-gray-300 transition duration-150 ease-in-out hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring disabled:opacity-25">
                        Create
                    </button>
                </form>
            </div>
        </Transition>
        <Transition name="slide-fade">
            <div v-if="showEdit" class="bg-white h-screen absolute top-0 right-0 w-4/12 p-5">
                <div class="flex justify-between">
                    <div>
                        Edit Tugas Baru
                    </div>
                    <div @click="closeEdit">
                        X
                    </div>
                </div>

                <form class="space-y-6" @submit.prevent="saveCompanyEdit">
                    <div class="space-y-4 rounded-md shadow-sm">
                        <div>
                            <label for="email" class="block text-sm font-medium text-gray-700">
                                Tanggal Deadline
                            </label>
                            <div class="mt-1">
                                <input type="date" name="email" id="email"
                                    class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
                                    v-model="company.email">
                            </div>
                        </div>

                        <div>
                            <label for="name" class="block text-sm font-medium text-gray-700">
                                Kategori Warna Tugas
                            </label>
                            <div class="mt-1">
                                <input type="color" name="name" id="name"
                                    class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
                                    v-model="company.name">
                            </div>
                        </div>

                        <div>
                            <label for="address" class="block text-sm font-medium text-gray-700">Address</label>
                            <div class="mt-1">
                                <textarea v-model="company.address" class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"></textarea>
                                
                            </div>
                        </div>

                        <div>
                            <label for="website" class="block text-sm font-medium text-gray-700">Website</label>
                            <div class="mt-1">
                                <input type="text" name="website" id="website"
                                    class="block mt-1 w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
                                    v-model="company.website">
                            </div>
                        </div>
                    </div>

                    <button type="submit"
                            class="inline-flex items-center px-4 py-2 text-xs font-semibold tracking-widest text-white uppercase bg-gray-800 rounded-md border border-transparent ring-gray-300 transition duration-150 ease-in-out hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring disabled:opacity-25">
                        Create
                    </button>
                </form>
            </div>
        </Transition>
        <div class="overflow-hidden overflow-x-auto min-w-full align-middle sm:rounded-md">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-6 xl:gap-8 ">
                <div @click="createTask()" class="flex justify-center flex-wrap content-center bg-white overflow-hidden shadow-sm sm:rounded-lg pt-8 pb-6 px-6 h-60">
                    <div>Tambah Tugas Baru</div>
                </div>
                <template v-for="item in companies" :key="item.id">
                    <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg p-5 h-60">
                        {{ item.name }}
                        <button @click="deleteCompany(item.id)"
                            class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150">
                            Delete
                        </button>
                        <button @click="editCompany(item.id)"
                            class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150">
                            Edit
                        </button>
                    </div>
                </template>
            </div>  
        </div>
        <div v-if="loading">
            Loading
        </div>
</template>

<script>
import useCompanies from "../../composables/companies";
import { onMounted } from "vue";
import { ref } from 'vue';
import { reactive } from "vue";

export default {
    setup() {
        const form = reactive({
            'name': '',
            'email': '',
            'address': '',
            'website': '',
        })

        const { errors, companies, company, loading, storeCompany, updateCompany, getCompany, getCompanies, destroyCompany } = useCompanies()
        const showCreate = ref(false)
        const showEdit = ref(false)
        const idCompany = ref('')

        onMounted(getCompanies)
        
        const createTask = async () => {
            showCreate.value = true
        }

        const closeCreate = async () => {
            showCreate.value = false
        }

        const closeEdit = async () => {
            showEdit.value = false
        }

        const deleteCompany = async (id) => {
            if (!window.confirm('Are you sure?')) {
                return
            }

            await destroyCompany(id);
            await getCompanies();
        }

        const editCompany = async (id) => {
            getCompany(id);
            idCompany.value = id
            showEdit.value = true
        }

        const saveCompany = async () => {
            await storeCompany({...form});
            await getCompanies();
            showCreate.value = false
        }

        const saveCompanyEdit = async () => {
            await updateCompany(company.value.id)
            showCreate.value = false
        }

        return {
            companies,
            loading,
            showCreate,
            showEdit,
            form,
            errors,
            company,
            idCompany,
            closeCreate,
            closeEdit,
            deleteCompany,
            saveCompanyEdit,
            editCompany,
            createTask,
            saveCompany
        }
    }
}
</script>
<style>
    /*
    Enter and leave animations can use different
    durations and timing functions.
    */
    .slide-fade-enter-active {
        transition: all 0.3s ease-out;
    }

    .slide-fade-leave-active {
        transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
    }

    .slide-fade-enter-from,
    .slide-fade-leave-to {
        transform: translateX(20px);
        opacity: 0;
    }
</style>