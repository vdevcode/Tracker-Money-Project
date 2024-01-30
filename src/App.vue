<template>
  <div class="p-4">
    <Header />
    <div class="my-2">
      <Balance :totalAmount="totalAmount" />
      <IncomeExpenses :income="income" :expense="expense" />
      <TransactionList
        :transactions="transactions"
        @deletedTransaction="deletedTransaction"
      />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed } from "vue";
import { useToast } from "vue-toastification";
const Toast = useToast();
const transactions = ref([
  {
    id: 1,
    text: "Giày Nike",
    amount: -19.99,
  },
  {
    id: 2,
    text: "Giày Hot",
    amount: 11.99,
  },
  {
    id: 3,
    text: "Áo Candy",
    amount: -12.99,
  },
  {
    id: 4,
    text: "Áo Hoodie",
    amount: 124.5,
  },
]);

//Tổng chi tiêu
const totalAmount = computed(() => {
  // Giả sử transactions là một ref hoặc reactive object
  //accumulator (biến tích lũy)
  return transactions.value.reduce((accumulator, transaction) => {
    return accumulator + transaction.amount;
  }, 0);
});

//thu nhap
const income = computed(() => {
  // Giả sử transactions là một ref hoặc reactive object
  //accumulator (biến tích lũy)
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0);
});

//chi phi
const expense = computed(() => {
  // Giả sử transactions là một ref hoặc reactive object
  //accumulator (biến tích lũy)
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((accumulator, transaction) => {
      return accumulator + transaction.amount;
    }, 0);
});

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  Toast.success("Thêm giao dịch thành công!");
};

const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000);
};

const deletedTransaction = (id) => {
  transactions.value = transactions.value.filter((transaction) => 
    transaction.id != id
  )
  Toast.success('Bạn đã xoá giao dịch này thành công!') 
};
</script>
