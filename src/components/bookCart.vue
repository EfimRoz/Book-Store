<template>
        <div v-if="item['quantity'] > 0" class="card is-fullwidth" data-id="item.id">
              <header class="card-header">
                <p class="card-header-title">
                  {{item.title}}
                </p>
              </header>
              <div class="card-content">
                <div class="content">
                  Quantity: {{item.quantity}}
                </div>
              </div>
              <footer class="card-footer">
                <a class="card-footer-item" @click="addItem()">+</a>
                <a class="card-footer-item" @click="removeItem()">-</a>
                <a class="card-footer-item" @click="thrashItem()">Clear</a>
              </footer>
            </div>
</template>
<script>
  export default {
    name: 'cart-list',
    props: ['item'],
      methods: {
          addItem(){
            this.$emit('add');
        },
        removeItem(){
            this.$emit('remove');
        },
        thrashItem(item){
            console.log('It all went to shit');
            this.$emit('thrash');
        }
        // deleteBook(){
      //       console.log('Request Delete');
        //      this.$emit('delete');
        //  }
      }
  }
</script>