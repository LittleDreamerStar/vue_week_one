<script setup>
import Button from 'primevue/button'
import InputText from 'primevue/inputtext'

import { ref } from 'vue'

const data = ref([
  {
    key: crypto.randomUUID(),
    title: '冬瓜檸檬',
    describe: '清新冬瓜配上新鮮檸檬',
    price: 55,
    stock: 34
  },
  {
    key: crypto.randomUUID(),
    title: '珍珠奶茶',
    describe: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    key: crypto.randomUUID(),
    title: '翡翠檸檬',
    describe: '綠茶與檸檬的完美結合',
    price: 50,
    stock: 20
  },
  {
    key: crypto.randomUUID(),
    title: '四季春茶',
    describe: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 0
  },
  {
    key: crypto.randomUUID(),
    title: '阿薩姆奶茶',
    describe: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    key: crypto.randomUUID(),
    title: '檸檬冰茶',
    describe: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    key: crypto.randomUUID(),
    title: '芒果綠茶',
    describe: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    key: crypto.randomUUID(),
    title: '抹茶拿鐵',
    describe: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])

const editTitleValue = ref('')

const addTempTitle = (e) => {
  editTitleValue.value = { ...e }
}

const enterTempTitle = () => {
  data.value = data.value.map((temp) =>
    temp.key === editTitleValue.value.key ? editTitleValue.value : temp
  )
  editTitleValue.value = ''
}
</script>

<template>
  <h1 style="margin: 20px auto; text-align: center">Vue Week1</h1>
  <hr />
  <table style="width: 80%; margin: 0 auto">
    <thead>
      <tr>
        <th scope="col" style="width: 30%">品項</th>
        <th scope="col" style="width: 40%">描述</th>
        <th scope="col" style="width: 10%">價格</th>
        <th scope="col" style="width: 20%">庫存</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in data" :key="item.key">
        <td style="width: 30%; text-align: center; user-select: none">
          <div style="display: flex; align-items: center">
            <Button
              icon="pi pi-file-edit"
              severity="info"
              style="margin-right: 10px"
              @click="addTempTitle(item)"
            />
            {{ item.title }}
          </div>
        </td>
        <td style="width: 40%; text-align: center; user-select: none">{{ item.describe }}</td>
        <td style="width: 10%; text-align: center; user-select: none">
          {{ item.price }}
        </td>
        <td style="width: 20%; text-align: center">
          <Button label="-" :disabled="item.stock <= 0" type="button" @click="item.stock--" />
          <span style="width: 30px; display: inline-block; line-height: 35px; user-select: none">{{
            item.stock
          }}</span>
          <Button label="+" type="button" @click="item.stock++" />
        </td>
      </tr>
    </tbody>
  </table>
  <hr />
  <div v-if="editTitleValue.title" style="margin: 20px auto; text-align: center">
    <InputText type="text" v-model="editTitleValue.title" />
    <Button
      label="確定"
      type="button"
      severity="success"
      style="margin: 0 20px"
      @click="enterTempTitle"
    />
    <Button label="取消" type="button" severity="warning" @click="editTitleValue = ''" />
  </div>
</template>
