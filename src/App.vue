<template>
  <div class="page-content" style="margin-top: -60px;">
    <div class="container-fluid">
      <Header />
      <Balance :total="+total" :totalInRiel="+totalInRiel" />
    </div>
  </div>
  <IncomeExpenses :income="+income" :expenses="+expenses" />
  <div class="page-content">
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

const toast = useToast();
const transactions = ref([]);

onMounted(() => {
  const saveTransaction = JSON.parse(localStorage.getItem("transactions"));
  if (saveTransaction) {
    transactions.value = saveTransaction;
  }
});

//Get Total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});
const totalInRiel = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount * 4124;
  }, 0);
});

//Get Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//Get Expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//Add Transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  toast.success("Transaction Added");
  saveTransactionToLocalStorage();
};

//generateUniqueId
const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000000000000);
};

//handleTransactionDeleted
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
  toast.success("Transaction deleted");
  saveTransactionToLocalStorage();
};

//save to local storage
const saveTransactionToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>
