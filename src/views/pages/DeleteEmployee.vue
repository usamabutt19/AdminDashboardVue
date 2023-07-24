<script>
import PageWrapper from '@/components/PageWrapper.vue';

export default {

    data() {
        return {
            title: 'Delete Employee',
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
        searchEmployee() {
            // Here you can implement the logic to search for the employee based on the provided `searchEmployeeEmail`
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
            if (employeeData.employee_id === this.searchEmployeeEmail) {
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
            console.log('Deleting Employee:', this.foundEmployee.employee_id);

            // You can send a request to your server to delete the employee record
        },
        goBack() {
            // Clear the foundEmployee data and reset the search form
            this.foundEmployee = null;
            this.searchEmployeeEmail = '';
            this.searched = false;
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
                <input type="email" id="employee_id" v-model="searchEmployeeEmail" required>
                <button v-on:click="dummyTrue" class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
                    Search Employee
                </button>
            </form>
        </div>
        <!-- If employee is found, show the employee details form -->
        <div v-if="foundEmployee">
            <div class="flex gap-16">
                <div class="flex-1 flex flex-col">
                    <label for="employee_id">Employee Email:</label>
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
                <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-red-500 shadow-lg hover:bg-red-600" @click="deleteEmployee">
                    Delete Employee
                </button>
                <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" @click="dummyNull">
                    Go Back
                </button>
            </div>
        </div>
        <!-- If employee is not found and search performed, show error message -->
        <div v-if="searched && !foundEmployee">
            <p class="text-red-500">Employee not found.</p>
            <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" @click="goBack">
                Go Back
            </button>
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

input[type='email']
 {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

/* Styling for the read-only employee details */
p {
    background-color: #f1f1f1;
    padding: 8px;
    border-radius: 5px;
    margin-bottom: 5px;
}

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
</style>
