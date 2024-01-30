<template>
  <div class="">
    <div class="mt-4 mb-2 border-b-[2px] boder-black">
      <h3>Thêm giao dịch mới</h3>
    </div>
    <div class="">
      <form action="" @submit.prevent="onSubmit">
        <!-- div1 -->
        <div class="mt-2">
          <label for="text">Tên</label>
          <br />
          <input
            class="outline-none border border-black rounded-md p-2 w-full"
            type="text"
            placeholder="Tên sản phẩm cần thêm..."
            v-model="text"
          />
        </div>
        <!-- div2 -->
        <div class="mt-2">
          <label for="text">Số tiền</label>
          <p>(âm - chi phí, dương - thu nhập)</p>
          <input
            class="outline-none border border-black rounded-md p-2 w-full"
            type="text"
            placeholder="Ví dụ: -10000"
            v-model="amount"
          />
        </div>
        <button
          class="justify-center flex bg-green-700 text-white w-full mt-4 py-2 rounded-md"
        >
          Thêm giao dịch
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const toast = useToast();
const text = ref("");
const amount = ref("");

const emit = defineEmits(["transactionSubmitted"]);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Vui lòng điền vào trường đầy đủ!");
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmitted", transactionData);
  text.value = "";
  amount.value = "";
};
</script>
