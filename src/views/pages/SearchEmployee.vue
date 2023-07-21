<script>
import PageWrapper from '@/components/PageWrapper.vue';

export default {
    // components: {
    //   PageWrapper,
    // },
    data() {
        return {
            title: "Search Employees",
            searchEmployeeId: "",
            searchFirstName: "",
            searchEmail: "",
            searchDepartment: "",
            searchResults: [], // To store search results
            employees: [ // Replace this array with your actual employee data or fetch from API
                {
                    id: 1,
                    first_name: "John",
                    last_name: "Doe",
                    email: "john.doe@example.com",
                    department: "HR",
                },
                {
                    id: 2,
                    first_name: "Jane",
                    last_name: "Smith",
                    email: "jane.smith@example.com",
                    department: "Finance",
                },
                // Add more employees here
            ],
        };
    },
    methods: {
        searchEmployeeById() {
            this.searchResults = this.employees.filter((employee) =>
                employee.id.toString().includes(this.searchEmployeeId)
            );
        },
        searchEmployeeByFirstName() {
            this.searchResults = this.employees.filter((employee) =>
                employee.first_name.toLowerCase().includes(this.searchFirstName.toLowerCase())
            );
        },
        searchEmployeeByEmail() {
            this.searchResults = this.employees.filter((employee) =>
                employee.email.toLowerCase().includes(this.searchEmail.toLowerCase())
            );
        },
        searchEmployeeByDepartment() {
            this.searchResults = this.employees.filter((employee) =>
                employee.department.toLowerCase().includes(this.searchDepartment.toLowerCase())
            );
        },
    },
};
</script>
<template>
<PageWrapper title="Search Employees">
    <div class="search-form">
        <h2 class="font-extrabold text-xl">{{title}}</h2>
        <div class="search-field">
            <label for="employee_id">Search by Employee ID:</label>
            <input type="text" id="employee_id" v-model="searchEmployeeId" @input="searchEmployeeById">
            <button class="ml-8 p-2 w-36 gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">Search</button>
        </div>

        <div class="search-field">
            <label for="first_name">Search by First Name:</label>
            <input type="text" id="first_name" v-model="searchFirstName" @input="searchEmployeeByFirstName">
            <button class="ml-8 p-2 w-36 gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">Search</button>
        </div>

        <div class="search-field">
            <label for="email">Search by Email:</label>
            <input type="email" id="email" v-model="searchEmail" @input="searchEmployeeByEmail">
            <button class="ml-8 p-2 w-36 gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">Search</button>
        </div>

        <div class="search-field">
            <label for="department">Search by Department:</label>
            <select id="department" v-model="searchDepartment" @change="searchEmployeeByDepartment">
                <option value="">Select Department</option>
                <!-- Add your department options here -->
            </select>
            <button class="ml-8 p-2 w-36 gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">Search</button>
        </div>

        <!-- Display search results here if needed -->
        <!-- For simplicity, we will just log the search results -->
        <div v-if="searchResults.length">
            <h3>Search Results:</h3>
            <ul>
                <li v-for="employee in searchResults" :key="employee.id">
                    {{ employee.first_name }} {{ employee.last_name }} ({{ employee.email }}) - Department: {{ employee.department }}
                </li>
            </ul>
        </div>
    </div>
</PageWrapper>
</template>

  
<style scoped>
/* Styling for the search form wrapper */
.search-form {
    margin: 20px 100px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.search-field {
    margin-bottom: 1rem;
}

label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input[type="text"],
input[type="email"],
select {
    width: 60%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

select {
    /* Adjust the height of the select element if needed */
    height: 40px;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    margin-bottom: 0.5rem;
}
</style>
