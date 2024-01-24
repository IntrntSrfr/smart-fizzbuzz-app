<template>
    <table id="infinite-scroll">
        <tr v-for="number in nums" :key="number" class="r">
            <td>
                {{ number }}
            </td>
            <td>
                {{ fizzBuzz(number) }}
            </td>
        </tr>
    </table>
</template>

<script setup lang="ts">
import { ref } from 'vue';
const nums = ref(Array.from(Array(100).keys()))

const checkScroll = () => {
    const scrollPercentage = (window.scrollY / (document.documentElement.scrollHeight - window.innerHeight)) * 100;
    if (scrollPercentage >= 95) addMoreNumbers()
}

const fizzBuzz = (n: number): number | string => {
    if (n % 15 == 0) return "FizzBuzz";
    else if (n % 3 == 0) return "Fizz";
    else if (n % 5 == 0) return "Buzz";
    else return "";
}

const addMoreNumbers = () => {
    let currentLength = nums.value.length;
    for (let i = 1; i <= 10; i++) {
        nums.value.push(currentLength + i);
    }
};

window.addEventListener("scroll", checkScroll)
</script>

<style>
#infinite-scroll {
    text-align: center;
    border-collapse: collapse;
    width: 200px;
    overflow-y: auto;
    font-size: 1.5em;
}

table tr {
    transition: 0.2s;
}

table tr:hover {
    background-color: #ffffff28;
}
</style>
