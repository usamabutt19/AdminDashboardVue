<script>
import PageWrapper from '@/components/PageWrapper.vue';
import axios from 'axios';

export default {
    // components: {
    //   PageWrapper,
    // },
    data() {
        return {
            title: "Search Employees",
            title1: "Employee Data",
            searchEmployeeId: "",
            searchFirstName: "",
            searchEmail: "",
            searchDepartment: "",
            foundEmployee: null,
            searchEmailResult: [],
            searchDepartmentResults: [],
            topRecords: []
        };
    },
    methods: {

        async searchEmployeeByEmail() {
            try {
                // API endpoint URL
                const emailData = {
                    field: "email",
                    searchfield: this.searchEmail
                };

                const apiUrl = "http://192.168.137.151:5000/searchuser";

                const response = await axios.post(apiUrl, emailData, {
                    headers: {
                        'Content-Type': 'application/json', // Set the Content-Type header to JSON
                    },
                });

                console.log('Response from API:', response.data);
                this.searchEmailResult = response.data
                this.foundEmployee = true

            } catch (error) {
                // Handle any errors that occur during the API call
                console.error('Error Searching employee:', error);

            }
        },

        async searchEmployeeByDepartment() {
            try {
                // API endpoint URL
                const emailData = {
                    field: "Departments",
                    searchfield: this.searchDepartment
                };

                const apiUrl = "http://192.168.137.151:5000/searchuser";

                const response = await axios.post(apiUrl, emailData, {
                    headers: {
                        'Content-Type': 'application/json', // Set the Content-Type header to JSON
                    },
                });

                this.searchDepartmentResults = response.data.sort((b, a) =>
                    new Date(a.hire_date) - new Date(b.hire_date)
                );

                this.topRecords = this.searchDepartmentResults.slice(0, 6);
                this.foundEmployee = true

            } catch (error) {
                // Handle any errors that occur during the API call
                console.error('Error Searching employee:', error);

            }
        },
        goback() {
            this.foundEmployee = false
            this.searchDepartmentResults = []
            this.searchEmailResult = []
            this.topRecords = []
            this.searchEmail = ""
            this.searchDepartment = ""
        }

    },
};
</script>
<template>
<PageWrapper title="Search Employees">
    <div class="search-form">
        <h2 v-if="!foundEmployee" class="font-extrabold text-xl">{{title}}</h2>

        <div v-if="!foundEmployee" class="search-field">
            <label for="email">Search by Email:</label>
            <input type="email" id="email" v-model="searchEmail">
            <button class="ml-8 p-2 w-36 gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit" v-on:click="searchEmployeeByEmail">Search</button>
        </div>
        <div v-if="foundEmployee && !searchDepartment.length">
            <h2 class="font-extrabold text-xl">{{title1}}</h2>
            <div class="flex gap-16">

                <div class="flex-1 flex flex-col">
                    <label for="employee_id">Employee ID:</label>
                    <p>{{ searchEmailResult.Employee_id }}</p>
                    <label for="first_name">First Name:</label>
                    <p>{{ searchEmailResult.first_name }}</p>
                    <label for="hire_date">Department: </label>
                    <p>{{ searchEmailResult.Department }}</p>
                    <label for="hire_date">Job Position: </label>
                    <p>{{ searchEmailResult.job_title }}</p>
                </div>
                <div class="flex-1 flex flex-col">
                    <label for="employee_email">Employee Email:</label>
                    <p>{{ searchEmailResult.email }}</p>
                    <label for="last_name">Last Name:</label>
                    <p>{{ searchEmailResult.last_name }}</p>
                    <label for="phone_number">Phone Number:</label>
                    <p>{{ searchEmailResult.phone_number }}</p>
                    <label for="hire_date">Job Location: </label>
                    <p>{{ searchEmailResult.location }}</p>
                </div>
            </div>
            <button class=" mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit" v-on:click="goback">Go Back</button>

        </div>
        <div v-if="!foundEmployee" class="search-field">
            <label for="first_name">Search by First Name:</label>
            <input type="text" id="first_name" v-model="searchFirstName" @input="searchEmployeeByFirstName">
            <button class="ml-8 p-2 w-36 gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">Search</button>
        </div>

        <div v-if="!foundEmployee" class="search-field">
            <label for="department">Search by Department:</label>
            <select id="department" v-model="searchDepartment" required>
                <option value="">Select Department</option>
                <option value="HR">HR</option>
                <option value="Sales">Sales</option>
                <option value="Finance">Finance</option>
                <option value="Executives">Executives</option>
                <option value="Technical">Technical</option>
            </select>
            <button class="ml-8 p-2 w-36 gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit" v-on:click="searchEmployeeByDepartment">Search</button>
        </div>

        <!-- Display search results here if needed -->
        <!-- For simplicity, we will just log the search results -->
        <div v-if="searchDepartment.length && foundEmployee">
            <h2 class="font-extrabold text-xl">{{this.searchDepartmentResults[0].Department}} Department</h2>
            <div class="table-container">
                <table class="employee-table">
                    <thead>
                        <tr>
                            <th>Email</th>
                            <th>First Name</th>
                            <th>Phone Number</th>
                            <th>Job Position</th>
                            <th>Location</th>
                            <th>Salary</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="employee in searchDepartmentResults" :key="employee.email">
                            <td class="truncate">{{ employee.email }}</td>
                            <td>{{ employee.first_name }}</td>
                            <td>{{ employee.phone_number }}</td>
                            <td>{{ employee.job_title }}</td>
                            <td>{{ employee.location }}</td>
                            <td>{{ employee.salary }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <button class=" mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit" v-on:click="goback">Go Back</button>
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
    margin-bottom: 0.25rem;
    margin-top: 1rem;
}

input[type="text"],
input[type="email"],
select {
    width: 60%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    height: 40px;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    margin-bottom: 0.5rem;
}

.table-container {
    max-height: 400px;
    /* Adjust the maximum height of the table container */
    overflow-y: auto;
}

.employee-table {
    width: 100%;
    border-collapse: collapse;
}

.employee-table th,
.employee-table td {
    padding: 8px;
    border: 1px solid #ccc;
    text-align: left;
}

.employee-table th {
    background-color: #f2f2f2;
    font-weight: bold;
}

.truncate {
    max-width: 150px;
    /* Adjust the maximum width of each cell to avoid excessive width */
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
</style>
