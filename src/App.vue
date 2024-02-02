<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import AddTransaction from './components/AddTransaction.vue';
import {ref, computed} from   'vue'


const transactions = ref([])

// const transactions = ref([
//     {id:1, text: 'Paycheck', amount: 699.99},
//     {id:2, text: 'Food', amount: -20},
//     {id:3, text: 'Bills', amount: -200},
//     {id:4, text: 'Video Game', amount: -54.11},
//     {id:5, text: 'Tax Return', amount: 3000},


// ])

//get total

const total = computed(()=>{
    return transactions.value.reduce((acc,transaction)=>{
        return acc + transaction.amount

    }, 0)
})
//get income - adding positive vals
const income = computed(()=> {
    return transactions.value
    .filter((transaction)=>transaction.amount > 0)
    .reduce((acc, transaction)=>{
        return acc+transaction.amount
    },0)
})

//get expenses - addin all negative vals
const expense = computed(()=> {
    return transactions.value
    .filter((transaction)=>transaction.amount < 0)
    .reduce((acc, transaction)=>{
        return acc+transaction.amount
    },0)
})

//handle trans submitted

const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
        text: transactionData.text,
        amount: transactionData.amount,

    })
}
</script>

<template>
    <Header></Header>
    <div class="container">
        <Balance :total="total"></Balance>
        <IncomeExpenses :income="income" :expense="expense"></IncomeExpenses>
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted"></AddTransaction>
        <!-- {{ transactions }} -->
    </div>
</template>