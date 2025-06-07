<template>
  <div class="company-form">
    <form @submit.prevent="submitForm" class="max-w-sm mx-auto">
      <div class="mb-5">
        <label
          for="name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Company Name</label
        >
        <input
          type="text"
          id="name"
          v-model="company.name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
      </div>
      <div class="mb-5">
        <label
          for="email"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Company Email</label
        >
        <input
          type="email"
          id="email"
          v-model="company.email"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
      </div>
      <div class="mb-5">
        <label
          for="address"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Company Address</label
        >
        <input
          type="text"
          id="address"
          v-model="company.address"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
      </div>
      <div class="mb-5">
        <label
          for="phone"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >Company Phone</label
        >
        <input
          type="text"
          id="phone"
          v-model="company.phone"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
      </div>

      <button
        type="submit"
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
      >
        {{ editMode ? "Update" : "Create" }} Company
      </button>
    </form>

    <!-- Display List of Companies -->

    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
      <table
        class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
        v-if="companies.length" width="100%"
      >
        <thead
          class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
        >
          <tr>
            <th scope="col" class="px-6 py-3">Company Name</th>
            <th scope="col" class="px-6 py-3">
              <div class="flex items-center">
                Company Email
                <a href="#"
                  ><svg
                    class="w-3 h-3 ms-1.5"
                    aria-hidden="true"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M8.574 11.024h6.852a2.075 2.075 0 0 0 1.847-1.086 1.9 1.9 0 0 0-.11-1.986L13.736 2.9a2.122 2.122 0 0 0-3.472 0L6.837 7.952a1.9 1.9 0 0 0-.11 1.986 2.074 2.074 0 0 0 1.847 1.086Zm6.852 1.952H8.574a2.072 2.072 0 0 0-1.847 1.087 1.9 1.9 0 0 0 .11 1.985l3.426 5.05a2.123 2.123 0 0 0 3.472 0l3.427-5.05a1.9 1.9 0 0 0 .11-1.985 2.074 2.074 0 0 0-1.846-1.087Z"
                    /></svg
                ></a>
              </div>
            </th>
            <th scope="col" class="px-6 py-3">
              <div class="flex items-center">
                
                <a href="#"
                  ><svg
                    class="w-3 h-3 ms-1.5"
                    aria-hidden="true"
                    xmlns="http://www.w3.org/2000/svg"
                    fill="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M8.574 11.024h6.852a2.075 2.075 0 0 0 1.847-1.086 1.9 1.9 0 0 0-.11-1.986L13.736 2.9a2.122 2.122 0 0 0-3.472 0L6.837 7.952a1.9 1.9 0 0 0-.11 1.986 2.074 2.074 0 0 0 1.847 1.086Zm6.852 1.952H8.574a2.072 2.072 0 0 0-1.847 1.087 1.9 1.9 0 0 0 .11 1.985l3.426 5.05a2.123 2.123 0 0 0 3.472 0l3.427-5.05a1.9 1.9 0 0 0 .11-1.985 2.074 2.074 0 0 0-1.846-1.087Z"
                    /></svg
                ></a>
              </div>
            </th>
            <th scope="col" class="px-6 py-3">
              <span class="sr-only">Edit</span>
            </th>
          </tr>
        </thead>
        <tbody>

          <tr v-for="company in companies" :key="company.id"
            class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 border-gray-200"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
            {{ company.name }} 
            </th>
            <td class="px-6 py-4">
              <a
                href="#"
                class="font-medium text-blue-600 dark:text-blue-500 hover:underline"
                >{{ company.email }}</a
              >
            </td>
            <td class="px-6 py-4 text-right">
              <button @click="editCompany(company.id)">Edit</button>
              <button @click="deleteCompany(company.id)">Delete</button>
            </td>
          </tr>
         
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "@/axios";

export default {
  data() {
    return {
      company: {
        name: "",
        email: "",
        address: "",
        phone: "",
      },
      companies: [],
      editMode: false,
      companyId: null,
    };
  },
  created() {
    this.loadCompanies();
  },
  methods: {
    submitForm() {
      if (this.editMode) {
        this.updateCompany();
      } else {
        this.createCompany();
      }
    },
    createCompany() {
      axios
        .post("/companies", this.company)
        .then((response) => {
          alert("Company created successfully!");
          this.loadCompanies();
          this.resetForm();
        })
        .catch((error) => {
          console.error(error);
          alert("Failed to create company.");
        });
    },
    updateCompany() {
      axios
        .put(`/companies/${this.companyId}`, this.company)
        .then((response) => {
          alert("Company updated successfully!");
          this.loadCompanies();
          this.resetForm();
        })
        .catch((error) => {
          console.error(error);
          alert("Failed to update company.");
        });
    },
    loadCompanies() {
      axios
        .get("/companies")
        .then((response) => {
          this.companies = response.data.data;
        })
        .catch((error) => {
          console.error(error);
          alert("Failed to load companies.");
        });
    },
    loadCompanyData(id) {
      this.editMode = true;
      this.companyId = id;
      axios
        .get(`/companies/${id}`)
        .then((response) => {
          this.company = response.data.data;
        })
        .catch((error) => {
          console.error(error);
          alert("Failed to load company data.");
        });
    },
    editCompany(id) {
      this.loadCompanyData(id);
    },
    deleteCompany(id) {
      if (confirm("Are you sure you want to delete this company?")) {
        axios
          .delete(`/companies/${id}`)
          .then(() => {
            alert("Company deleted successfully!");
            this.loadCompanies();
          })
          .catch((error) => {
            console.error(error);
            alert("Failed to delete company.");
          });
      }
    },
    resetForm() {
      this.company = {
        name: "",
        email: "",
        address: "",
        phone: "",
      };
      this.editMode = false;
      this.companyId = null;
    },
  },
};
</script>

<style scoped>
.company-form {
  max-width: 400px;
  margin: auto;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

button {
  margin-left: 10px;
}
</style>
