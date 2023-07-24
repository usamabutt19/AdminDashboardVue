<script>
import PageWrapper from '@/components/PageWrapper.vue'

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
                addDepartment: "",
                addLocation: "",
                jobPosition: ""
            }
        };
    },
    methods: {
        addEmployee() {
            // Here you can implement the logic to submit the form and add the employee
            // For simplicity, we will just log the employee data
            console.log(
                // employee_id: this.employee_id,
                "dataFields of Add Employee: ", this.dataFields
            );

            // You can send the data to your server or perform other actions here
            // For example, you might make an API call to add the employee to your database
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
                    <select id="department" v-model="dataFields.addDepartment" @change="searchEmployeeByDepartment" required>
                        <option value="">Select Department</option>
                        <option value="HR">HR</option>
                        <option value="Sales">Sales</option>
                        <option value="Finance">Finance</option>
                        <option value="Exectives">Exectives</option>
                        <option value="Technicle">Technicle</option>
                    </select>
                    <label for="location">Office Location</label>
                    <select id="location" v-model="dataFields.addLocation" @change="searchEmployeeByDepartment" required>
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
                    <input type="text" id="last_name" v-model="dataFields.last_name" required>
                    <label for="phone_number">Phone Number:</label>
                    <input type="tel" id="phone_number" v-model="dataFields.phone_number" required>
                    <label for="salary">Salary:</label>
                    <input type="number" id="salary" v-model="dataFields.salary" inputmode="numeric" required>
                    <label for="position">Job Position</label>
                    <select id="position" v-model="dataFields.jobPosition" @change="searchEmployeeByDepartment" required>
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
