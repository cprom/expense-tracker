<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue';
import {ref, computed} from 'vue'

const transactions = ref([
  {id: 1, text:'Paycheck', amount: 699.99},
  {id: 2, text:'Food', amount: -20},
  {id: 3, text:'Bills', amount: -200},
  {id: 4, text:'Video Game', amount: -54.11},
  {id: 4, text:'Tax Return', amount: 3000},

])

//get the total
const total = computed(() => {
  return transactions.value.reduce( (acc, transactions) => {
    return acc + transactions.amount
  }, 0)
})

// get the income by adding all positive value
const income = computed(() => {
  return transactions.value.filter((transactions) => transactions.amount > 0).reduce((acc, transactions) => {
    return acc + transactions.amount
  }, 0)
})

//get the expense by adding all negative value
const expense = computed(() => {
  return transactions.value.filter((transactions) => transactions.amount < 0).reduce((acc, transactions) => {
    return acc + transactions.amount
  }, 0)
})


</script>

<template>
<Header></Header>
<div class="container">
  <Balance :total="total"></Balance>
  <IncomeExpenses :income="income" :expense="expense"></IncomeExpenses>
</div>
</template>