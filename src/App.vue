
<template >

  <div id="app">
    <h2>Các loại điện thoại Vertu | Iphone không đủ tuổi :v</h2>
  <table width="100%" border="1" >
    <tr>
      <th>STT</th>
      <th>Tên Sản Phẩm</th>
      <th>Giá</th>
      <th></th>
    </tr>
    <tr v-for="product in products" :key="product.message" >
      <td style="text-align: center; width:50px">{{product.code }} </td>
      <td>{{product.name }} </td>
      <td>{{product.price | formatNumber}}</td>
      <td><button class="btn" @click="addTocartProduct(product)">Mua</button></td>
    </tr>
  </table>
    <h2>Sản phẩm của đại gia khi chọn :v</h2>
     <table width="100%" border="1" >
    <tr>
      <th>Tên Sản Phẩm</th>
      <th>Giá</th>
      <th>Số Lượng</th>
      <th></th>
    </tr>
    <tr v-for="CartProduct in CartProducts" :key="CartProduct.message" >
      <td>{{CartProduct.name }}</td>
      <td>{{CartProduct.price | formatNumber}}</td>
  
      <td><input type="text" v-model="CartProduct.quality"></td>
      <td><button class="button button3" @click="deleteCartProduct(CartProduct)">xoá</button></td>
    </tr>
       <tr>
     <td colspan="4" v-show="CartProducts.length == 0">Bạn chưa có sản phẩm trong giỏ hàng </td>
   </tr>
   <tr>
     <td colspan="4"  v-show="CartProducts.length >0"> Tổng giá : {{Cart | formatNumber}}</td>
   </tr>
      <tr>
     <td colspan="4" v-show="CartProducts.length >0">Khuyến mại : {{sale | formatNumber}}%</td>
   </tr>
         <tr>
     <td colspan="4" v-show="CartProducts.length >0">Thanh Toán:  {{Pay | formatNumber }}</td>
   </tr>
  </table>
  <button>Thanh Toán</button>
  </div>
</template>

<script>
import Vue from 'vue';
var numeral = require("numeral");

  Vue.filter("formatNumber", function (value) {
    return numeral(value).format("0,0"); // displaying other groupings/separators is possible, look at the docs
  });

export default {
data(){
  return{
    products:[
            { code:'1', name:'Vertu Signature S Red Leather',price:'310000000',quality:1},
             { code:'2', name:'Vertu Signature S Yellow Gold Diamond Bag Keys',price:'1450000000',quality:1},
              { code:'3', name:'Vertu Signature S Rose Gold',price:'7500000000',quality:1},
             { code:'4', name:'ertu Constellation Quest 8GB Blue Limited',price:'356000000',quality:1},
    ],
    CartProducts:[],
    Cart:0,
    Pay:0,
    sale:0,
  }
},
  methods:{
 
    addTocartProduct(product)
    {    
             if(this.CartProducts.indexOf(product) !== -1)
       {
         window.alert('Đã Tồn Tại sản phẩm');
         return;
       }
       this.CartProducts.push(product);
    },
    
    
    deleteCartProduct(CartProduct)
    {
        var positionCartProduct =this.CartProducts.indexOf(CartProduct);
        console.log(positionCartProduct);
        this.CartProducts.splice(positionCartProduct,1);
    },
    caculateCart()
    {

        this.CartProducts.forEach((product)=>{
          this.Cart += product.price *product.quality; 
        });
     

        // tính giảm giá
        this.sale =0;
        if (this.Cart>400000000)
        {
           
          this.sale=10;
        }
        // tính tổng giá
        this.Pay = this.Cart*(100-this.sale)/100;
      
    }
  },
  watch:
  {
    
    CartProducts: {
         handler(){
           this.caculateCart();
         },
        deep:true,
        immediate:true
    }
   
  },
  

}

</script>

<style>
.btn {
background-color: #4CAF50;
border: none;
color: white;
padding: 15px 32px;
cursor: pointer;
}
.button3 {
  background-color: #f44336;
      border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
  } /* Red */ 

</style>
