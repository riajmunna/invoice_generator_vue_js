<script setup>
import { reactive } from 'vue';
import {invoice1, invoice2} from './data/data.js';
let data = reactive({
  sender: '',
  billTo: '',
  shipTo: '',
  invoiceNumber: '',
  date: '',
  dueDate: '',
  additionalNote: '',
  items: [
    {
      description: '',
      quantity: '',
      rate: '',
      amount: ''
    }
  ],
  notes: '',
  terms: '',
  subtotal: '',
  tax: '',
  total: '',
  dueBalance: ''
})

function addMoreItem() {
  data.items.push({
    description: '',
    quantity: '',
    rate: '',
    amount: ''
  })
}

function deleteItem(){
  data.items.pop();
}

function subTotal(){
  let subtotal = 0;
  data.items.forEach(element => {
    subtotal += element.amount;
  });
  data.subtotal = subtotal;
  return subtotal;
}


</script>

<template>
  <section class="mx-auto container bg-white border border-gray-400 min-h-screen p-12 text-black">
    <div class="flex justify-between">
      <div class="flex flex-col space-y-5 w-1/2s">
        <div class=" ">
          <img class="w-40"
            src="https://www.shutterstock.com/image-vector/invoice-typographic-stamp-sign-badge-600w-1027820257.jpg"
            alt="">
        </div>
        <p class="mt-5 text-black">
          Sender
        </p>
        <textarea name="" id="" cols="30" rows="2" v-model="data.sender"></textarea>
        <div class="flex space-x-2 text-black">
          <div class="flex flex-col">
            <span>Bill to</span>
            <textarea name="" id="" cols="30" rows="2" v-model="data.billTo"></textarea>
          </div>
          <div class="flex flex-col">
            <span>Ship to</span>
            <textarea name="" id="" cols="30" rows="2" v-model="data.shipTo"></textarea>
          </div>
        </div>
      </div>
      <div class="flex flex-col w-1/2 items-end">
        <h1 class="mt-12 text-4xl uppercase text-right mb-5 text-black">Invoice</h1>
        <input class="w-[200px] text-right" type="text" placeholder="Invoice Number" v-model="data.invoiceNumber">
        <div class="mt-10 flex-y-5 text-right space-y-3 w-full text-black">
          <p>
            <span>Date</span>
            <input class="ml-2 w-[200px]" v-model="data.date">
          </p>
          <p>
            <span>Due Date</span>
            <input class="ml-2 w-[200px]" v-model="data.dueDate">
          </p>
          <p>
            <span>Additional Note</span>
            <input class="ml-2 w-[200px]" type="text" v-model="data.additionalNote">
          </p>
        </div>
      </div>
    </div>
    <div class="mt-20">
      <table class="table-auto w-full">
        <tr class="bg-gray-800 text-left text-white">
          <th class="p-2">Action</th>
          <th class="p-2 pl-5 w-1/2">Item</th>
          <th class="p-2">Quantity</th>
          <th class="p-2">Rate</th>
          <th class="p-2 w-[200px] text-right pr-5">Amount</th>
        </tr>
        <tr v-for="(item, index) in data.items" :key="index">
          <td class="py-1">
            <button class="w-full pl-2 text-white" @click="deleteItem">Delete</button>
          </td>
          <td class="py-1">
            <input class="w-full pl-5" type="text" placeholder="Description" v-model="item.description" />
          </td>
          <td class="">
            <input class="w-full" type="number" placeholder="Quantity" v-model="item.quantity" />
          </td>
          <td class="">
            <input class="w-full" type="number" placeholder="Rate" v-model="item.rate">
          </td>
          <td class="py-1 pr-5 text-right text-gray-800">
            $ {{ item.amount = item.quantity * item.rate }}
          </td>
        </tr>
      </table>
      <button class="mt-5 bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded" @click="addMoreItem">
        Add More
      </button>
      <button class="ml-3 mt-5 bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded" @click="Object.assign(data,invoice1)">
        Import Invoice 1
      </button>
      <button class="ml-3 mt-5 bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded" @click="Object.assign(data,invoice2)">
        Import Invoice 2
      </button>
    </div>
    <div class="mt-[200px]">
      <div class="flex justify-between">
        <div class="flex flex-col space-y-5 w-1/2 text-black">
          <span>Notes</span>
          <textarea name="" id="" cols="30" rows="2" v-model="data.notes"></textarea>
          <span>Terms</span>
          <textarea name="" id="" cols="30" rows="2" v-model="data.terms"></textarea>
        </div>
        <div class="flex flex-col w-1/2 items-end">
          <div class="mt-10 flex-y-5 text-right space-y-3 w-full text-black">
            <p>
              <span>Subtotal</span>
              <input readonly class="focus:ring-0 focus:ring-offset-0 text-right ml-2 pr-4 w-[200px] border-0" :value="subTotal()"
                placeholder="Subtotal">
            </p>
            <p>
              <span>Tax (%)</span>
              <input type="number" class="tax text-right w-[200px] ml-2" v-model="data.tax">
            </p>
            <p>
              <span>Total</span>
              <input readonly class="focus:ring-0 focus:ring-offset-0 text-right ml-2 pr-4 w-[200px] border-0" :value="data.total = data.subtotal + (data.subtotal * data.tax / 100)"
                placeholder="Total">
            </p>
            <!-- <p>
              <span>Balace Due</span>
              <input readonly class="focus:ring-0 focus:ring-offset-0 text-right ml-2 pr-4 w-[200px] border-0"
                placeholder="Balance">
            </p> -->
          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<style scoped>
input,
textarea {
  border: 1px solid #ddd !important;
  padding: 5px;
  border-radius: 5px;
}

input.tax::-webkit-outer-spin-button,
input.tax::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}</style>
