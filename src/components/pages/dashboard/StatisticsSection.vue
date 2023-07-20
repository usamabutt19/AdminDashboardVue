<script setup>
import QuiclStatisticsCard from '@/components/QuiclStatisticsCard.vue'

const employeesData = [4, 3, 10, 9, 29, 19, 22, 9, 12, 7, 19, 5, 13]
const departmentsData = [4, 3, 10, 9, 29, 19, 22, 9, 12, 7, 19, 5, 13].reverse()
const countriesData = [4, 3, 10, 9, 29, 19, 22, 9, 12, 7, 19, 5, 13]
//const growthData = [4, 3, 10, 9, 29, 19, 22, 9, 12, 7, 19, 5, 13]
</script>

<template>
    <section class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-4 place-content-center">
        <h2 class="sr-only">Quick statistics</h2>

        <!-- employees card -->
        <QuiclStatisticsCard
            title="Employees"
            :chartData="employeesData"
            result="12.4k"
            percentage="32.40%"
            :actions="[{ title: 'View', to: '#' }]"
            icon="mdi:account-group-outline"
        />
       
        <!-- departments card -->
        <QuiclStatisticsCard
            title="Departments"
            :chartData="departmentsData"
            result="128"
            status="success"
            percentage="2.10%"
            :actions="[{ title: 'View', to: '#' }]"
        />

        <!-- countries card -->
        <QuiclStatisticsCard
            title="Countries"
            :chartData="countriesData"
            result="34"
            status="success"
            percentage="0.60%"
            :actions="[{ title: 'View', to: '#' }]"
           
        />

        <!-- Growth card -->
        <!-- <QuiclStatisticsCard
            title="Growth"
            :chartData="growthData"
            result="15.6%"
            percentage="7.20%"
            :actions="[{ title: 'View', to: '#' }]"
            icon="mdi:chart-pie"
        /> -->
    </section>
</template>
