<script>
import bookService from '../book.service';
import cartService from '../cart.service';
import bookFilter from './bookFilter';
import bookPreview from './bookPreview';
import bookCart from './bookCart';
export default {
    components:{
        bookFilter,
        bookPreview,
        bookCart
    },
  name: 'book-list',
  data () {
     return {
            books: null,
            selectedBook : null,
            editedBook: null,
            isCreateMode : false
        }
  },
  

    created() {
        bookService.getBooks().then(books => this.books = books)
    },
    methods: {
        selectBook(book) {
            this.selectedBook = book;
        },
        resetSelected() {
            this.selectedBook = null;
        },
        selectNext() {
            this.selectedBook = bookService.getNext(this.selectedBook);
        },
        editBook(book) {
            console.log('Editing the book', book)
            this.editedBook = book;
        },
        deleteBook(book) {
            bookService.deleteBook(book);
        },
        saveBook(book) {
            bookService.saveBook(book);
            this.editedBook = null;
            this.isCreateMode =false;
        },
        cancelBookEdit(){
            this.isCreateMode = false;
            this.editedBook = null;
        },
        addToCart(book){
            console.log('add to cart');
            cartService.addToCart(book);
            console.log(book);
        },
        removeFromCart(book){
            cartService.substractFromCart(book.id);
        },
        trashTheBook(book){
            cartService.clearItem(book.id);
            
        }
    }
}
</script>
<template>
    
        <section v-if="books">
            <h2>We have {{books.length}} Books</h2>
            <button @click="isCreateMode=true">+</button>
            <book-filter></book-filter>
            <ul>
                <book-preview v-for="currBook in books" 
                    @click.native="selectBook(currBook)" 
                    @edit="editBook(currBook)"
                    @delete="deleteBook(currBook)"
                    @addToCart="addToCart(currBook)"
                    :book="currBook">
                </book-preview>
            </ul>
            <book-details v-if="selectedBook"
                 @close="resetSelected"
                 @next="selectNext"
                 :book="selectedBook">
            </book-details>

             <book-edit v-if="editedBook || isCreateMode"
                 :book="editedBook"
                 @save="saveBook"
                 @cancel="cancelBookEdit()">
            </book-edit>
            <cart-list v-for="book in books"
                        :item="book"
                        @add="addToCart(book)"
                        @remove="removeFromCart(book)"
                        @thrash="trashTheBook(book)">
            </cart-list>

        </section>
        
</template>
