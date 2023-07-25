<script>
import PageWrapper from '@/components/PageWrapper.vue'
import axios from 'axios';
import {
    successToast,
    errorToast
} from '@/toast'

export default {
    data() {
        return {
            dataFields: {
                title: "Add Employee",
                first_name: "",
                last_name: "",
                email: "",
                phone_number: "",
                hire_date: "",
                salary: null,
                department: "",
                location: "",
                jobPosition: ""
            },
            // jobPositions: [{
            //         department: 'HR',
            //         position: 'HR Associate'
            //     },
            //     {
            //         department: 'HR',
            //         position: 'HR Manager'
            //     },
            //     {
            //         department: 'Sales',
            //         position: 'SalesMan'
            //     },
            //     {
            //         department: 'Sales',
            //         position: 'Sales Manager'
            //     },
            //     {
            //         department: 'Marketing',
            //         position: 'Marketing Associate'
            //     },
            //     {
            //         department: 'Marketing',
            //         position: 'Marketing Manager'
            //     },
            //     {
            //         department: 'Executives',
            //         position: 'Assistant Director'
            //     },
            //     {
            //         department: 'Executive',
            //         position: 'Director'
            //     },
            //     {
            //         department: 'Technical',
            //         position: 'Electrical Engineer'
            //     },
            //     {
            //         department: 'Technical',
            //         position: 'Software Engineer'
            //     },
            // ],
            jobPositions: {
                'HR': ['HR Associate', 'HR Manager'],
                'Sales': ['SalesMan', 'Sales Manager'],
                'Marketing': ['Marketin Associate', 'Marketing Manager'],
                'Executives': ['Assistant Director', 'Director'],
                'Technical': ['Software Engineer', 'Electrical Engineer', "Lead Engineer"],
            },
            locations: {
                'HR Associate': ['Islamabad, Pakistan', 'Okazaki, Japan', 'Ottawa, Canada', 'Berlin, Germany', 'London, United Kindom', 'DC, United States of America'],
                'HR Manager': ['Islamabad, Pakistan', 'Okazaki, Japan', 'Ottawa, Canada', 'Berlin, Germany', 'London, United Kindom', 'DC, United States of America'],

                'Sales Manager': ['Karachi, Pakistan', 'Tokyo, Japan', 'Berlin, Germany', 'DC, United States of America', 'Ottawa, Canada', 'Canberra, Australia'],
                'SalesMan': ['Karachi, Pakistan', 'Tokyo, Japan', 'Berlin, Germany', 'DC, United States of America', 'Ottawa, Canada', 'Canberra, Australia'],

                'Marketing Associate': ['Karachi, Pakistan', 'Tokyo, Japan', 'Berlin, Germany', 'DC, United States of America', 'Ottawa, Canada', 'Canberra, Australia'],
                'Marketing Manager': ['Karachi, Pakistan', 'Tokyo, Japan', 'Berlin, Germany', 'DC, United States of America', 'Ottawa, Canada', 'Canberra, Australia'],

                'Assistant Director': ['Islamabad, Pakistan'],
                'Director': ['Islamabad, Pakistan'],
                'Software Engineer': ['Islamabad, Pakistan', 'Lahore, Pakistan', 'Karachi, Pakistan', 'Beijing, China', 'Kuala Lumpur, Malaysia', 'Tokyo, Japan', 'Okazaki, Japan', 'Berlin, Germany', 'London, United Kindom', 'DC, United States of America', 'Ottawa, Canada', 'Brasilia, Brazil', 'Cape Town, South Africa', 'Canberra, Australia'],
                'Electrical Engineer': ['Islamabad, Pakistan', 'Lahore, Pakistan', 'Karachi, Pakistan', 'Beijing, China', 'Kuala Lumpur, Malaysia', 'Tokyo, Japan', 'Okazaki, Japan', 'Berlin, Germany', 'London, United Kindom', 'DC, United States of America', 'Ottawa, Canada', 'Brasilia, Brazil', 'Cape Town, South Africa', 'Canberra, Australia'],
                'Lead Engineer': ['Islamabad, Pakistan', 'Lahore, Pakistan', 'Karachi, Pakistan', 'Beijing, China', 'Kuala Lumpur, Malaysia', 'Tokyo, Japan', 'Okazaki, Japan', 'Berlin, Germany', 'London, United Kindom', 'DC, United States of America', 'Ottawa, Canada', 'Brasilia, Brazil', 'Cape Town, South Africa', 'Canberra, Australia'],
            },
            filteredJobPositions: [], // Initialize the filteredJobPositions array
            filteredLocations: [], // Initialize the filteredLocations array

        };
    },
    methods: {
        async addEmployee() {
            try {
                // API endpoint URL

                const employeeData = JSON.stringify(this.dataFields);

                //API endpoint URL
                const apiUrl = 'http://192.168.1.102:5000/newuser';

                // Make the API POST request using axios
                const response = await axios.post(apiUrl, employeeData, {
                    headers: {
                        'Content-Type': 'application/json', // Set the Content-Type header to JSON
                    },
                });
                // Log the response or handle it as needed
                console.log('Response from API:', response.data);
                // Show a success toast when the API call is successful
                successToast({
                    title: 'Employee Added',
                    text: 'The employee has been successfully added!',
                });

                // Clear form fields after successful submission
                // this.dataFields = {
                //     title: "Add Employee",
                //     first_name: "",
                //     last_name: "",
                //     email: "",
                //     phone_number: "",
                //     hire_date: "",
                //     salary: null,
                //     department: "",
                //     location: "",
                //     jobPosition: ""
                // };
            } catch (error) {
                // Handle any errors that occur during the API call
                console.error('Error adding employee:', error);
                errorToast({
                    title: 'Error',
                    text: 'An error occurred while adding the employee. Please try again later.',
                });
            }
        },
        filterJobPositions() {
            // Filter job Positions based on the selected department
            const department = this.dataFields.department;
            if (!department) return [];
            this.filteredJobPositions = this.jobPositions[department] || []
        },
        filtereJobLocations() {
            // Filter job Location based on the selected job Positions
            const jobPosition = this.dataFields.jobPosition;
            if (!jobPosition) return []; // Return an empty array if jobPosition is not selected

            this.filteredLocations = this.locations[jobPosition] || [];
        },
        searchEmployeeByDepartment() {
            // this.searchResults = this.employees.filter((employee) =>
            //     employee.department.toLowerCase().includes(this.searchDepartment.toLowerCase())
            // );
        },
    }
}
</script>

<template>
<PageWrapper title="AddEmployee">
    <!--  -->
    <div class="parent">
        <h2 class="font-extrabold text-xl">{{ dataFields.title }}</h2>
        <form @submit.prevent="addEmployee">

            <div class=" flex gap-16">
                <div class=" flex-1 flex flex-col">
                    <label for="first_name">First Name:</label>
                    <input type="text" id="first_name" v-model="dataFields.first_name" required>
                    <label for="email">Email:</label>
                    <input type="email" id="email" v-model="dataFields.email" required>
                    <label for="hire_date">Hire Date:</label>
                    <input type="date" id="hire_date" v-model="dataFields.hire_date" required>
                    <label for="department">Add Department:</label>
                    <select id="department" v-model="dataFields.department" @change="filterJobPositions" required>
                        <option value="">Select Department</option>
                        <option value="HR">HR</option>
                        <option value="Sales">Sales</option>
                        <option value="Marketing">Marketing</option>
                        <option value="Executives">Executives</option>
                        <option value="Technical">Technical</option>
                    </select>
                    <label for="location">Office Location</label>
                    <select id="location" v-model="dataFields.location" required>
                        <option value="">Select Location</option>
                        <option v-for="location in filteredLocations" :value="location" :key="location">{{ location }}</option>
                    </select>

                </div>
                <div class=" flex-1 flex flex-col">
                    <label for="last_name">Last Name:</label>
                    <input type="text" id="last_name" v-model="dataFields.last_name" required>
                    <label for="phone_number">Phone Number:</label>
                    <input type="tel" id="phone_number" v-model="dataFields.phone_number" required>
                    <label for="salary">Salary:</label>
                    <input type="number" id="salary" v-model="dataFields.salary" inputmode="numeric" required>
                    <label for="position">Job Position</label>
                    <select id="position" v-model="dataFields.jobPosition" @change="filtereJobLocations" required>
                        <option value="">Select Job Position</option>
                        <option v-for="position in filteredJobPositions" :value="position" :key="position">{{ position }}</option>
                    </select>
                </div>

            </div>

            <button class=" mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">Add Employee</button>
        </form>
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

input[type="text"],
input[type="email"],
input[type="tel"],
input[type="number"],
input[type="date"] {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

input[type="number"] {
    -moz-appearance: textfield;
}
</style>
