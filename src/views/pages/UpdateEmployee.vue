<template>
<PageWrapper :title="title">
    <!--  -->
    <div class="parent">
        <h2 class="font-extrabold text-xl">{{ title }}</h2>
        <!-- If employee is not found, show the search form -->
        <div v-if="!foundEmployee">
            <form @submit.prevent="searchEmployee">
                <label for="employee_id">Search Employee by ID:</label>
                <input type="text" id="employee_id" v-model="searchEmployeeId" required>
                <button v-on:click="dummyTrue" class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
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
                <label for="employee_id">Employee ID:</label>
                <input type="text" id="employee_id" v-model="foundEmployee.employee_id" disabled>

                <div class="flex gap-16">
                    <div class="flex-1 flex flex-col">
                        <label for="first_name">First Name:</label>
                        <input type="text" id="first_name" v-model="foundEmployee.first_name" required>
                        <label for="email">Email:</label>
                        <input type="email" id="email" v-model="foundEmployee.email" required>
                        <label for="hire_date">Hire Date:</label>
                        <input type="date" id="hire_date" v-model="foundEmployee.hire_date" required>
                    </div>
                    <div class="flex-1 flex flex-col">
                        <label for="last_name">Last Name:</label>
                        <input type="text" id="last_name" v-model="foundEmployee.last_name" required>
                        <label for="phone_number">Phone Number:</label>
                        <input type="tel" id="phone_number" v-model="foundEmployee.phone_number" required>
                        <label for="salary">Salary:</label>
                        <input type="number" id="salary" v-model="foundEmployee.salary" inputmode="numeric" required>
                    </div>
                </div>
<div class="flex gap-4">
                <button class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
                    Update Employee
                </button>
                <button
                v-on:click="dummyNull"
                class="mt-4 p-2 w-36 flex justify-center gap-2 rounded-md transition-colors text-white bg-purple-500 shadow-lg hover:bg-purple-600" type="submit">
                    Update Another Employee
                </button>
            </div>

            </form>
        </div>
    </div>
</PageWrapper>
</template>

  
<script>
import PageWrapper from '@/components/PageWrapper.vue';

export default {

    data() {
        return {
            title: 'Update Employee',
            searchEmployeeId: '',
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
        updateEmployee() {
            // Here you can implement the logic to submit the form and update the employee
            // For simplicity, we will just log the updated employee data
            console.log(this.foundEmployee);

            // You can send the data to your server or perform other actions here
            // For example, you might make an API call to update the employee in your database
        },
    },
};
</script>

  
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
