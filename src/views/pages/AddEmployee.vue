<script>
import PageWrapper from '@/components/PageWrapper.vue'

export default {
    data() {
        return {
            title: "Add Employee",
            employee_id: "",
            first_name: "",
            last_name: "",
            email: "",
            phone_number: "",
            hire_date: "",
            salary: null,
        };
    },
    methods: {
        addEmployee() {
            // Here you can implement the logic to submit the form and add the employee
            // For simplicity, we will just log the employee data
            console.log({
                employee_id: this.employee_id,
                first_name: this.first_name,
                last_name: this.last_name,
                email: this.email,
                phone_number: this.phone_number,
                hire_date: this.hire_date,
                salary: this.salary,
            });

            // You can send the data to your server or perform other actions here
            // For example, you might make an API call to add the employee to your database
        },
    },
};
</script>

<template>
<PageWrapper title="AddEmployee">
    <!--  -->
    <div class="parent">
        <h2 class="font-extrabold text-xl">{{ title }}</h2>
        <form @submit.prevent="addEmployee">
            <label for="employee_id">Employee ID:</label>
            <input type="text" id="employee_id" v-model="employee_id" required>

            <div class=" flex gap-16">
                <div class=" flex-1 flex flex-col">
                    <label for="first_name">First Name:</label>
                    <input type="text" id="first_name" v-model="first_name" required>
                    <label for="email">Email:</label>
                    <input type="email" id="email" v-model="email" required>
                    <label for="hire_date">Hire Date:</label>
                    <input type="date" id="hire_date" v-model="hire_date" required>
                </div>
                <div class=" flex-1 flex flex-col">
                    <label for="last_name">Last Name:</label>
                    <input type="text" id="last_name" v-model="last_name" required>
                    <label for="phone_number">Phone Number:</label>
                    <input type="tel" id="phone_number" v-model="phone_number" required>
                    <label for="salary">Salary:</label>
                    <input type="number" id="salary" v-model="salary" inputmode="numeric" required>
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
