<script setup>
import {computed, ref} from "vue";

const products = ref ([
   { id: 1,
    name: 'Iphone',
    date: '20.11.2024',
    count: 100,
    price:1500
},
{
    id:2,
    name: 'Sumsung',
    date: '20.11.2024',
    count: 100,
    price:1500
},
{
    id:3,
    name: 'Xiaomi',
    date: '12.11.2024',
    count: 120,
    price:180
}
])

const name = ref ('');
const date = ref ('');
const count = ref (1);
const price =ref(0);

const addProduct = () => {
    if (name.value && date.value && count.value && price.value){
        products.value.push(   
        
        {
            id: Date.now(),
            name: name.value,
            date: (new Date(date.value)).toLocaleDateString(),
            count: count.value,
            price: price.value,

        }
    )
    }
}
const removeProduct = (id) => {
    products.value=products.value.filter((product)=>product.id != id);
}

const totalSum = computed(() => {
    return products.value.reduce((sum,product) => sum + (product.price * product.count), 0)
    });
</script>

<template>
      <div class="col">
            <h1 class="text-center mt-4">Учет товаров</h1>
            <form action="">
                <form class="mb-3">
                    <div class="mb-3">
  <label for="name" class="form-label">Название</label>
  <input type="text" class="form-control" id="name" >
</div>
<div class="mb-3">
    <label for="date" class="form-label">Дата добавления</label>
  <input type="date" class="form-control" id="date">
</div>
<div>
<label for="count" class="form-label">Количество</label>
  <input type="number" class="form-control" id="count">
</div>
<div>
    <label for="price" class="form-label">Цена</label>
  <input type="number" class="form-control" id="price">
</div>
<div class="text-center mb-3">
    <button type="button" class="btn btn-secondary">Добавить</button>
</div>
    </form>
            </form>
        </div>

    <div class="row row-cols-1 row-cols-md-3 g-4">
 <div class="col" v-for="product in products" :key="product.id">
<div class="card h-100">
<div class="card-body">
<h5 class="card-title">{{ product.name }}</h5>
<p class="card-text">{{ product.date }}</p>
<p class="card-text">{{ product.price }}</p>
<p class="card-text">{{ product.count }}</p>
</div>
<div class="card-footer">
    <button @click="removeProduct(product.id)" class="btn btn-outline-danger">Удалить</button>
</div>
</div>
</div>
</div>
<h3 class="text-end">общая сумма:{{ totalSum }}</h3>

</template>

<style>
</style>
