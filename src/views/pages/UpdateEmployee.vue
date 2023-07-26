<script>
import PageWrapper from '@/components/PageWrapper.vue';

export default {

    data() {
        return {
            dataFields: {
                title: 'Update Employee',
                first_name: "",
                last_name: "",
                email: "",
                phone_number: "",
                hire_date: "",
                salary: null,
                addDepartment: "",
                addLocation: "",
                jobPosition: ""
            },
            searchEmployeeEmail: '',
            foundEmployee: null,
            searched: false,
        };
    },
    methods: {
        dummyTrue() {
            this.foundEmployee = true
        },
        dummyNull() {
            this.foundEmployee = null
        },

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
                this.searchDepartmentResults = response.data
                this.foundEmployee = true


            } catch (error) {
                // Handle any errors that occur during the API call
                console.error('Error Searching employee:', error);
            }
        },

        updateEmployee() {
            // Here you can implement the logic to submit the form and update the employee
            // For simplicity, we will just log the updated employee data
            console.log(this.dataFields);

            // You can send the data to your server or perform other actions here
            // For example, you might make an API call to update the employee in your database
        },
    },
};
</script>

<template>
<PageWrapper :title="title">
    <!--  -->
    <div class="parent">
        <h2 class="font-extrabold text-xl">{{ dataFields.title }}</h2>
        <!-- If employee is not found, show the search form -->
        <div v-if="!foundEmployee">
            <form @submit.prevent="searchEmployee">
                <label for="employee_email">Search Employee by Email:</label>
                <input type="email" id="employee_email" v-model="searchEmployeeEmail" required>
                <button v-on:click="searchEmployeeByEmail" class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
                    Search Employee
                </button>
            </form>
            <div v-if="searched && !foundEmployee">
                <p class="text-red-500">Employee not found.</p>
            </div>
        </div>
        <!-- If employee is found, show the employee details form -->
        <div v-else>
            <form @submit.prevent="updateEmployee">
                <div class=" flex gap-16">
                    <div class=" flex-1 flex flex-col">
                        <label for="first_name">First Name:</label>
                        <input type="text" id="first_name" v-model="dataFields.first_name">
                        <label for="email">Email:</label>
                        <input type="email" id="email" v-model="dataFields.email">
                        <label for="hire_date">Hire Date:</label>
                        <input type="date" id="hire_date" v-model="dataFields.hire_date">
                        <label for="department">Add Department:</label>
                        <select id="department" v-model="dataFields.addDepartment" @change="searchEmployeeByDepartment">
                            <option value="">Select Department</option>
                            <option value="HR">HR</option>
                            <option value="Sales">Sales</option>
                            <option value="Marketing">Marketing</option>
                            <option value="Executives">Executives</option>
                            <option value="Technical">Technical</option>
                        </select>
                        <label for="location">Office Location</label>
                        <select id="location" v-model="dataFields.addLocation" @change="searchEmployeeByDepartment">
                            <option value="">Select Loaction</option>
                            <option value="Islamabad, Pakistan">Islamabad, Pakistan</option>
                            <option value="Beijing, China">Beijing, China</option>
                            <option value="Kuala Lumpur, Malaysia">Kuala Lumpur, Malaysia</option>
                            <option value="Tokyo, Japan">Tokyo, Japan</option>
                            <option value="Okazaki, Japan">Okazaki, Japan</option>
                            <option value="Berlin, Germany">Berlin, Germany</option>
                            <option value="London, United Kindom">London, United Kindom</option>
                            <option value="DC, United States of America">DC, United States of America</option>
                            <option value="Ottawa, Canada">Ottawa, Canada</option>
                            <option value="Brasilia, Brazil">Brasilia, Brazil</option>
                            <option value="Cape Town, South Africa">Cape Town, South Africa</option>
                        </select>
                    </div>
                    <div class=" flex-1 flex flex-col">
                        <label for="last_name">Last Name:</label>
                        <input type="text" id="last_name" v-model="dataFields.last_name">
                        <label for="phone_number">Phone Number:</label>
                        <input type="tel" id="phone_number" v-model="dataFields.phone_number">
                        <label for="salary">Salary:</label>
                        <input type="number" id="salary" v-model="dataFields.salary" inputmode="numeric">
                        <label for="position">Job Position</label>
                        <select id="position" v-model="dataFields.jobPosition" @change="searchEmployeeByDepartment">
                            <option value="">Select Job Position</option>
                            <option value="Electrical Engineer">Electrical Engineer</option>
                            <option value="Software Engineer">Software Engineer</option>
                            <option value="Lead Engineer">Lead Engineer</option>
                            <option value="HR Associate">HR Associate</option>
                            <option value="HR Manager">HR Manager</option>
                            <option value="Accountant">Accountant</option>
                            <option value="Marketing Manager">Marketing Manager</option>
                            <option value="Assistant Director">Assistant Director</option>
                            <option value="Director">Director</option>
                            <option value="SalesMan">SalesMan</option>
                            <option value="Sales Manager">Sales Mananger</option>
                        </select>
                    </div>

                </div>
                <div class="flex gap-4">
                    <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
                        Update Employee
                    </button>
                    <button v-on:click="dummyNull" class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
                        Update Another Employee
                    </button>
                </div>

            </form>
        </div>
    </div>
</PageWrapper>
</template>

<style scoped>
/* Styling for the form wrapper */
.parent {
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

form {
    display: grid;
    gap: 10px;
}

label {
    font-weight: bold;
    margin-bottom: 0.5rem;
    margin-top: 1rem;
}

input[type='text'],
input[type='email'],
input[type='tel'],
input[type='number'],
input[type='date'] {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

input[type='number']::-webkit-inner-spin-button,
input[type='number']::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

input[type='number'] {
    -moz-appearance: textfield;
}
</style>
