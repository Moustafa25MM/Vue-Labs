<template>
  <div>
  <div class="d-flex justify-content-between align-items baseline p-2 my-2 bg-dark">
    <a href="#" style="text-decoration: none;" @click.prevent ="isListVisible=false">Books</a>
    <div class="d-flex align-items-baseline justify-content-between">
        <p class="mx-2" style="color: yellow;">[{{list.items.length}}] <template v-if="list.items.length==1">book</template>  <template v-else>books</template> with total price[ {{ formatCurrency(getTotalPrice()) }}]</p>
        <button class="btn btn-primary" @click="isListVisible = true">Show Wish List</button>
    </div>
</div>

<div class="row m-auto text-center" v-if="isListVisible == false">
  <div class="card border m-auto" style="width: 25rem;" v-for="book in books">
      <img :src="book.image" :title="book.author">
      <div class="d-flex justify-content-between align-items-baseline">
          <p>{{book.category}}</p>
          <p>{{book.author}}</p>
      </div>
      <div class="d-flex justify-content-between align-items-baseline">
          <p :class="[book.pages>100 ? 'more': '' , book.pages < 100 ? 'less':'']">Pages: {{book.pages}}</p>
          <p>price: {{ formatCurrency(book.price)}}</p>
      </div>
      <div class="card-footer">
          <div class="d-flex justify-content-between align-items-baseline">
              <p>ISBN: {{book.isbn}}</p>
              <button  class="btn btn-primary" @click.once="addToList(book)">Add to List</button>
          </div>
      </div>
  </div>
</div>
<div class="row text-center" v-if="isListVisible == true">
  <h3 class="text-danger text-center" v-if="list.items.length==0" >
      No Books Yet!!!!!
  </h3>
  <table class="table table-striped table-bordered text-center" v-else>
      <thead>
          <tr>
              <th>Name</th>
              <th>Category</th>
              <th>Author</th>
              <th>Pages</th>
              <th>Price</th>
              <th>Isbn</th>
              <th>Action</th>
              <th>Total Price</th>
          </tr>
      </thead>
      <tbody>
          <tr v-for="item in list.items">
              <td>{{item.book.name}}</td>
              <td>{{item.book.category}}</td>
              <td>{{item.book.author}}</td>
              <td>{{item.book.pages}}</td>
              <td>{{item.book.price}}</td>
              <td>{{item.book.isbn}}</td>
              <td><button class="btn btn-danger" @click="removeFromList(item)" >Remove</button></td>
              <td>{{ formatCurrency(item.quantity*item.book.price)}}</td>
          </tr>
      </tbody>
      <tfoot>
          <tr>
              <th colspan="4">Total Price</th>
              <th colspan="2">{{ formatCurrency(getTotalPrice()) }}</th>
          </tr>
          <tr>
              <th colspan="4">Total Taxes</th>
              <th colspan="2">{{ formatCurrency(getTotalPrice()*0.1) }}</th>
          </tr>
          <tr>
              <th colspan="4">Grand Total</th>
              <th colspan="2">{{ formatCurrency(getTotalPrice() + getTotalPrice()*0.1)}}</th>
          </tr>
      </tfoot>
  </table>
</div>
</div>
</template>

import books from "../books";
<script>

export default {
  data:()=>({
                books:books,
                isListVisible:false,
                list:{
                    items:[]
                },
                isVisible:true,
            }),
            methods:{
                addToList(book){
                    this.list.items.push({
                        book:book,
                        quantity:1
                    })
                },
                getTotalPrice(){
                    let result =0;
                    for (let index = 0; index < this.list.items.length; index++) {
                       result += this.list.items[index].book.price*1
                        
                    }
                    return result;
                },
                removeFromList(item){
                    this.list.items.splice(this.list.items.findIndex(iitem=>iitem.book.isbn==item.book.isbn),1)
                },

                formatCurrency(value) {
                    return Intl.NumberFormat("ar-SA",{
                        style:'currency',
                        currency:'SAR',
                        maximumFractionDigits:0
                    }).format(value);  

                },
                removeButton(book){
                    this.isVisible = false;
                }
            }
};
</script>

<style>
.card {
  margin: 20px;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 8px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease-in-out;
}
.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.15), 0 15px 30px rgba(0, 0, 0, 0.2);
}
.card img {
  height: 300px;
  object-fit: cover;
  border-radius: 10px;
  margin-bottom: 10px;
}
.card p {
  margin: 0;
  font-size: 18px;
  font-weight: 600;
}
.card-footer {
  background-color: #f8f9fa;
  border-top: none;
  border-radius: 0 0 10px 10px;
  padding: 10px;
}
.card-footer button {
  font-size: 16px;
  font-weight: 600;
}
.more{
  color:green;
}
.less{
  color:red;
}
.more,.less{
  font-weight: bold;
}
</style>