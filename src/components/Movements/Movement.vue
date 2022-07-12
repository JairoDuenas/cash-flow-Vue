<template>
  <div class="movement">
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="action">
      <img src="@/assets/trash-icon.svg" alt="borrar" @click="remove" />
      <p
        :class="{
          red: isNegative,
          green: !isNegative,
        }"
      >
        {{ amountCurrency }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { toRefs, defineProps, defineEmits, computed } from "vue";

const currencyFormatter = new Intl.NumberFormat("es-CO", {
  style: "currency",
  currency: "COP",
});

const props = defineProps({
  id: {
    type: Number,
  },
  title: {
    type: String,
  },
  description: {
    type: String,
  },
  amount: {
    type: Number,
  },
});

const { id, title, description, amount } = toRefs(props);
const amountCurrency = computed(() => currencyFormatter.format(amount.value));
const isNegative = computed(() => amount.value < 0);
const emit = defineEmits(["remove"]);
const remove = () => {
  emit("remove", id.value);
};
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  font-style: normal;
  margin: 0;
  padding: 0;
}
h4 {
  font-weight: 500;
  font-size: 18px;
  line-height: 21px;
  margin-bottom: 8px;
  color: #5a5a5a;
}
p {
  font-weight: 300;
  font-size: 14px;
  line-height: 16px;
  color: #000000;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
  color: red;
}
.green {
  color: green;
}
</style>
