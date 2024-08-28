# Yemek-Sepeti

/*function addToCart(element) {
     let input = element.previousEelementSibling;  //select previous element in this case its input (coz we want to see value we write in input)

     console.log(input.value);    //once we click on add in items, value we put in input will be shown
} */
let allTotal = 0;   //start counting from zero. Its global variable, we can use it for all our countings we specify later
function addToCart(element) {
    let mainEl = element.closest('.single-item'); //we selected classes with all items (parents of those items) (beside input value we also need to see name and price of item)
    let price = mainEl.querySelector('.price').innerText; //we want to select the price (which is in <p> with class .price, so we put a dot coz its a class), by writing innerText we just display the text inside it, not whole sentence as it would show without adding innerText
    let name = mainEl.querySelector('h3').innerText;  //we also need to see the name of item in console 
    let quantity = mainEl.querySelector('input').value; //we also needd to see quantity of item we add. For input we use 'value' and for others 'innerText'
    
    /* query selector can be used on main elements that u previously select (element)
    and from the main element u select things inside of it (price, name, quantity...) */
    
    let cartItems = document.querySelector('.cart-items') //we dont use mainEl anymore to select, coz this class is in different element on the document, so we select it from document directly
    
    /* console.log(typeof(quantity)); >>>> it shows us its a string, to be able to count it we hv to convert it to number using parseInt*/

    if(parseInt(quantity) > 0) {
        /*cartItems.innerHTML += 'Added' + name;   
        now we want to add items inside cart (when we click on adding to buy them)
        you have to put += so it will keep adding items one after another without deleting previously added ones*/

      /*  cartItems.innerHTML +=  `Item: ${name} -     //add some html here to make it look better
                                Price: ${price} -
                                Quantity: ${quantity} -
                                Total: ${total}<br>`;     //we need to add total, set the counting when items are added in cart
        */

        cartItems.innerHTML += `<div class= "cart-single-item">
                                 <hr3>${name}</h3>
                                 <p>$${price} x ${quantity} = $<span>${total}</span></p> //put this total in a span so u can select it later
                                 <button onclick=:removeFromCart(this)" class="remove-item">Remove item</button>  //to select button give it a class, write this to specify (this button!). we want when we click on button to work (when u clcik it will remove items from cart)   
                                 </div>`;
        document.querySelector('.total').innerText = `Total: ${total}`  //this is total for one item, but we need all total, which we will put in the beginning of page
        allTotal += total;  //keep counting totals (+=) till u get allTotal 
        let total = price * parseInt(quantity); //convert quantity to number also
        
        price = price.substring(1);  //our price is a string (has $ in front), we have to remove $ sign, so we have just a number to count it. we remove $ sign with substring select 1 coz its in front
        price = parseInt(price); //convert string(price) to number
        element.innerText = 'Added to cart'; //once we add item on the page we want this 'Added to cart' to be written
        element.setAttribute('disabled', 'true'); //once we added the item we want to disable the button, to not be able to click it again
    } else {
        alert('Select quantity');    //if written number is < or = to 0 it will give us alert to 'select quantity
    }
    
    function removeFromCart(element) {
        let mainEl = element.closest('.cart-single-item');  //select things u want to be removed, name, price, quantity, all of them are inside .cart-single-item classes (all items have same class name)
        //mainEl.remove();  //used to remove, delete sth
        let price = mainEl.querySelector('p span').innerText; //we selected our total from the span, which is inside of <p>
        let name = mainEl.querySelector('h3').innerText;  //we also need to add name
        let vegetables = document.querySelectorAll('.single-item'); //select class in which are our items, so we can show them
        price = parsInt(price);   //convert this price to number
        allTotal -= price;    //now we do - in all total ( removing items)

        document.querySelector('.total').innerText = `Total: $${allTotal}`; //add new - counting in document to be written on page inside .total class
        mainEl.remove();
        vegetables.forEach(function(vege) {
            let itemName = vege.querySelector('.si-content h3').innerText;  //select the name of items which is in h3

            if(itemName === name) {
                vege.querySelector('actions input').value = 0;  //re add the value of 0 to input once we removed item
                vege.querySelector('actions button').removeAttribute('disabled'); //enable the button 
                vege.querySelector('action button').innerText = 'Add'; //write text add once its empty, ready to start over again adding process
            }
        });
} 
