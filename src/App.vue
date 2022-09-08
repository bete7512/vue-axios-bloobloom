<template>
  <div class="menuheader">
    <div class="menu">
        <div clas="button">
          menu
        </div>
      <div class="svg"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
          stroke="currentColor" class="w-12 h-12">
          <path stroke-linecap="round" stroke-linejoin="round"
            d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563 0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0 01-.84.61l-4.725-2.885a.563.563 0 00-.586 0L6.982 20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0 00-.182-.557l-4.204-3.602a.563.563 0 01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z" />
        </svg>
      </div>
    </div>
  </div>
  <table>
    <tr>
      <th>
      </th>
      <th>
        Spectacles Women
      </th>
      <th></th>
    </tr>
    <!-- //  -->
  <tr v-for="id in womens.glasses" :key="id">
  <td><img class="" :src="id.glass_variants[3].media[0].url" alt=""></td>
   <td><img :src="id.glass_variants[0].media[0].url" alt=""></td>
  <td><img :src=" id.glass_variants[2].media[0].url" alt=""></td>
  </tr>
  </table>
<div>{{consumed}}</div>
</template>
<script setup>
import { onMounted,ref } from 'vue';
import axios from 'axios'
const consumed = ref('')
const womens = ref('')
onMounted(()=>{
  axios
      .get('https://staging-api.bloobloom.com/user/v1/sales_channels/website/collections')
      .then(response => {
        (console.log(response.data))
        consumed.value = response.data
      })
      .catch(error => console.log(error))
})
onMounted(()=>{
  axios
      .get('https://staging-api.bloobloom.com/user/v1/sales_channels/website/collections/spectacles-men/glasses?sort[type]=collection_relations_position&sort[order]=asc&filters[lens_variant_prescriptions][]=fashion&filters[lens_variant_types][]=classic&page[limit]=12&page[number]=1&=')
      .then(response => {
        (console.log(response.data.glasses[0].glass_variants[0]))
        womens.value = response.data
      })
      .catch(error => console.log(error))
})
// console.log(consumed.value);
console.log(womens.value);
</script>
<style scoped>
.menheader {
  display: flex;
  margin-top: 3rem;
  justify-content: center;
}
.menu {
  display: flex;
  font-size: 30px;
  margin-top: 2rem;
  justify-content: left;
  font-weight: bold;
}
.svg {
  display: flex;
  padding-left: 700px;
  height: 20px;
  width: 20px;
}
.button:hover{
  color: aqua;
  text-decoration: underline;
}

table {
  border-collapse: collapse;
  width: 100%;
}
th{
  padding: 15px;
}
th,
td {
  text-align: left;
  border: 1px solid #000;
}
img{
  width:100%;
}

td{
  width: 33.333333%;
  height:200px;
}
</style>
