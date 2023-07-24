<script>
import PageWrapper from '@/components/PageWrapper.vue';

export default {

    data() {
        return {
            title: 'Employee History',
            searchEmployeeId: '',
            start_date: "",
            end_date: "",
            addDepartment: "",
            addLocation: "",
            jobPosition: "",
            foundEmployee: null,
            searched: false,
            showhistory: false
        };
    },
    methods: {
        dummyTrue() {
            this.foundEmployee = true
        },
        dummyNull() {
            this.foundEmployee = null
        },
        searchEmployee() {
            // Here you can implement the logic to search for the employee based on the provided `searchEmployeeId`
            // For simplicity, let's assume you already have the employee data fetched and stored in a variable named `employeeData`
            const employeeData = {
                employee_id: 'EMP001',
                first_name: 'John',
                last_name: 'Doe',
                email: 'john.doe@example.com',
                phone_number: '123-456-7890',
                hire_date: '2023-01-01',
                salary: 50000,
            };

            // Simulate the search result
            if (employeeData.employee_id === this.searchEmployeeId) {
                this.foundEmployee = {
                    ...employeeData
                };
                this.searched = true;
            } else {
                this.foundEmployee = null;
                this.searched = true;
            }
        },
        deleteEmployee() {
            // Here you can implement the logic to delete the employee
            // For simplicity, we will just log the employee_id of the employee to be deleted
            console.log('Employee:', this.foundEmployee.employee_id);

            // You can send a request to your server to delete the employee record
        },
        goBack() {
            // Clear the foundEmployee data and reset the search form
            this.foundEmployee = null;
            this.searchEmployeeId = '';
            this.searched = false;
        },
        addhistory() {
            this.showhistory = true;
            console.log({
                start_date: this.start_date,
                end_date: this.end_date,
                addDepartment: this.addDepartment,
                addLocation: this.addLocation,
                jobPosition: this.jobPosition,
            });
        },
        searchEmployeeByDepartment() {
            // this.searchResults = this.employees.filter((employee) =>
            //     employee.department.toLowerCase().includes(this.searchDepartment.toLowerCase())
            // );
        },
    },
};
</script>
<template>
<PageWrapper :title="title">
    <!--  -->
    <div class="parent">
        <h2 class="font-extrabold text-xl">{{ title }}</h2>
        <!-- If employee is not found and search not performed, show the search form -->
        <div v-if="!foundEmployee">
            <form @submit.prevent="searchEmployee">
                <label for="employee_id">Search Employee by Email:</label>
                <input type="text" id="employee_id" v-model="searchEmployeeId" required>
                <button v-on:click="dummyTrue" class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
                    Search Employee
                </button>
            </form>
        </div>
        <!-- If employee is found, show the employee details form -->
        <div v-if="foundEmployee && !showhistory">
            <div class="flex gap-16">
                <div class="flex-1 flex flex-col">
                    <label for="employee_id">Employee ID:</label>
                    <p>{{ foundEmployee.email }}</p>
                    <label for="first_name">First Name:</label>
                    <p>{{ foundEmployee.first_name }}</p>
                    <label for="hire_date">Department: </label>
                    <p>{{ foundEmployee.department }}</p>
                    <label for="hire_date">Job Position: </label>
                    <p>{{ foundEmployee.job_position }}</p>
                </div>
                <div class="flex-1 flex flex-col">
                    <label for="last_name">Last Name:</label>
                    <p>{{ foundEmployee.last_name }}</p>
                    <label for="phone_number">Phone Number:</label>
                    <p>{{ foundEmployee.phone_number }}</p>
                    <label for="hire_date">Job Location: </label>
                    <p>{{ foundEmployee.job_location }}</p>
                </div>
            </div>

            <div class="flex justify-between">
                <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-green-500 shadow-lg hover:bg-green-600" v-on:click="addhistory">
                    Add history
                </button>
                <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" @click="dummyNull">
                    Go Back
                </button>
            </div>
        </div>
        <!-- If employee is not found and search performed, show error message -->
        <div v-if="searched && !foundEmployee">
            <p class="text-red-500">Employee not found.</p>
            <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" @click="dummyNull">
                Go Back
            </button>
        </div>
        <!-- If employee is found, show the employee details form -->
        <div v-if="showhistory">
            <form class="" @submit.prevent="addhistory">

                <div class=" flex gap-16">
                    <div class=" flex-1 flex flex-col">
                        <label for="start_date">Start Date:</label>
                        <input type="date" id="start_date" v-model="start_date" required>
                        <label for="department">Add Department:</label>
                        <select id="department" v-model="addDepartment" @change="searchEmployeeByDepartment" required>
                            <option value="">Select Department</option>
                            <option value="HR">HR</option>
                            <option value="Sales">Sales</option>
                            <option value="Finance">Finance</option>
                            <option value="Exectives">Exectives</option>
                            <option value="Technicle">Technicle</option>
                        </select>
                        <label for="location">Office Location</label>
                        <select id="location" v-model="addLocation" @change="searchEmployeeByDepartment" required>
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
                        <label for="end_date">End Date:</label>
                        <input type="date" id="end_date" v-model="end_date" required>
                        <label for="position">Job Position</label>
                        <select id="position" v-model="jobPosition" @change="searchEmployeeByDepartment" required>
                            <option value="">Select Job Position</option>
                            <option value="Electrical Engineer">Electrical Engineer</option>
                            <option value="Software Engineer">Software Engineer</option>
                            <option value="Lead Engineer">Lead Engineer</option>
                            <option value="HR Associate">HR Associate</option>
                            <option value="HR Manager">HR Manager</option>
                            <option value="Accountant">Accountant</option>
                            <option value="Finance Manager">Finance Manager</option>
                            <option value="Assistant Director">Assistant Director</option>
                            <option value="Director">Director</option>
                            <option value="Sales Man">Sales Man</option>
                            <option value="Sales Manager">Sales Mananger</option>
                        </select>
                    </div>

                </div>

                <button class=" mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">Add History</button>
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

/* Styling for the read-only employee details */
p {
    background-color: #f1f1f1;
    padding: 8px;
    border-radius: 5px;
    margin-bottom: 5px;
}

/* .flex {
    display: flex;
    align-items: center;
} */

.gap-16 {
    gap: 16px;
}

.flex-1 {
    flex: 1;
}

.justify-between {
    justify-content: space-between;
}

button {
    cursor: pointer;
}

button[type='submit'] {
    display: inline-block;
}

.history_form {
    display: grid;
    gap: 10px;
}

.history_form label {
    font-weight: bold;
    margin-bottom: 0.5rem;
    margin-top: 1rem;
}

.history_form input[type="text"],
.history_form input[type="email"],
.history_form input[type="tel"],
.history_form input[type="number"],
.history_form input[type="date"] {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.history_form input[type="number"]::-webkit-inner-spin-button,
.history_form input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

.history_form input[type="number"] {
    -moz-appearance: textfield;
}
</style>
