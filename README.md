
<html>
<head>
  <title>Menu Calculator</title>
    <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 250vh;
      text-align: center;
    }
	.total-box {
		display: flex;
		justify-content: center; /* Center horizontally */
		align-items: center; /* Center vertically */
		margin-top: 20px;
	}}
	
	 .calculate-button {
      width: 150px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
    }
	
	.submit-button {
      width: 150px; /* Adjust the desired width */
      height: 40px; /* Adjust the desired height */
    }
	
	.reset-button {
      width: 150px; /* Adjust the desired width */
      height: 30px; /* Adjust the desired height */
    }
    
    h1 {
      margin-bottom: 20px;
    }
    
    h2 {
      margin-top: 20px;
    }
	
	h3 {
      border: 1px solid black; /* Adjust the border style as needed */
      padding: 5px; /* Add padding to create space around the heading */
    }
    
    .menu-items {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 10px;
      margin-bottom: 10px;
    }
    
    .menu-items div {
      display: flex;
      align-items: center;
    }
    
    .total-box {
      display: flex;
      justify-content: flex-end;
      align-self: Center;
      margin-top: 20px;
    }
    
    .button-container {
      display: flex;
      gap: 10px;
      margin-top: 20px;
    }
	
	.menu-items div img {
      width: 50px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
      margin-left: 10px; /* Add margin as per your preference */
    }
    {
    button {
      margin-top: 20px;
	}}}}}}
  </style>
  <script>
    function calculateTotal() {
    var total = 0;
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');

    checkboxes.forEach(function(checkbox) {
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);

      if (checkbox.value === '-25%') {
        var itemPrice = total * 0.25;
        total -= itemPrice;
      } else if (checkbox.value === '-30%') {
        var itemPrice = total * 0.3;
        total -= itemPrice;
      } else if (checkbox.value === '-50%') {
        var itemPrice = total * 0.5;
        total -= itemPrice;
      } else {
        total += price * quantity;
      }
    });

    var totalElement = document.getElementById('total');
    totalElement.textContent = total.toFixed(2);

    var discountTotalElement = document.getElementById('discount-total');
    var discount = total * 0.10;
    discountTotalElement.textContent = discount.toFixed(2);
  }


    
    function submitOrder() {
    var name = document.getElementById('name').value;
    if (name.trim() === '') {
      alert('Please enter a name.');
      return;
    }

    // Collect selected items and their quantities
    var selectedItems = [];
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');
    checkboxes.forEach(function (checkbox) {
      var itemName = checkbox.nextElementSibling.textContent;
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);
      selectedItems.push({ name: itemName, quantity: quantity, price: price });
    });

    var total = 0;
    var discountTotal = 0;

    selectedItems.forEach(function (item) {
      if (item.price < 0) {
        var discountPercentage = Math.abs(item.price);
        var itemDiscount = total * (discountPercentage / 100);
        discountTotal += itemDiscount;
      } else {
        total += item.price * item.quantity;
      }
    });

    var commission = (total * 0.15).toFixed(2);
    var totalWithDiscount = total - discountTotal;

    alert('Order submitted!');

    var discordWebhookURL = 'https://discord.com/api/webhooks/1205697839481749545/iRpz5OJe-oaSBWXr8XUxu1Npyu6NkNi78qPU9_r0VnxE5SoT5HR0M0fItBhvYAJBq4ax'

    var xhr = new XMLHttpRequest();
    xhr.open('POST', discordWebhookURL, true);
    xhr.setRequestHeader('Content-Type', 'application/json');

    var message = {
      content: 'New order!',
      embeds: [{
        title: 'Order Details',
        fields: [
          {
            name: 'Name',
            value: name,
            inline: true
          },
          {
            name: 'Total',
            value: '$' + totalWithDiscount.toFixed(2),
            inline: true
          },
          {
            name: 'Discount Total',
            value: '$' + discountTotal.toFixed(2),
            inline: true
          },
          {
            name: 'Commission (15%)',
            value: '$' + commission,
            inline: true
          },
          {
            name: 'Ordered Items',
            value: selectedItems.map(item => `${item.name} x${item.quantity} - $${(item.price * item.quantity).toFixed(2)}`).join('\n'),
            inline: false
          }
        ]
      }]
    };

    xhr.send(JSON.stringify(message));
  }

function resetCalculator() {
  var checkboxes = document.querySelectorAll('input[type="checkbox"]');
  var quantityInputs = document.querySelectorAll('input[type="number"]');
  
  checkboxes.forEach(function(checkbox) {
    checkbox.checked = false;
  });
  
  quantityInputs.forEach(function(quantityInput) {
    quantityInput.value = 1;
  });
  
  document.getElementById('total').textContent = '0.00';
}
	function submitAndReset() {
	submitOrder();
	resetCalculator();
}

  </script>
</head>
<body>
	
<div style="margin-bottom: 25px;"></div>
 
<body style="background-color:#FFA1F6;">
  <h1>Menu Calculator</h1>
  
  <h2>Menu Items</h2>

  <div style="margin-bottom: 10px;"></div>
  
  <h3>Food</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="150$">
    <label for="Velmachoice">Salad - $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">BLT - $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Turkey Sandwich - $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Beef Sandwich - $</label>150
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Crisp Sandwich - $</label>150
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="200$">
    <label for="Davechoice">Chocolate Pancakes - $</label>200
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="200$">
    <label for="Davechoice">Fruit Explosions - $</label>200
    <input type="number" value="1" min="1">
  </div>
  
   <h3>Beverage</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="150$">
    <label for="Velmachoice">Green Tea - $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Iced Coffee - $</label>150
    <input type="number" value="1" min="1">
  </div>

   <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Matcha Tea - $</label>150
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Boba Tea - $</label>150
    <input type="number" value="1" min="1">
  </div>

   <div>
    <input type="checkbox" id="Davechoice" value="200$">
    <label for="Davechoice">Pumpkin Spiced Latte - $</label>200
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="200$">
    <label for="Davechoice">Cat Tuccinos - $</label>200
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="200$">
    <label for="Davechoice">Fresh Lemonade - $</label>200
    <input type="number" value="1" min="1">
  </div>
 
   <h3>Dessert</h3>

  <div style="margin-bottom: 10px;"></div>
  
 <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Homemade Cookie - $</label>150
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Apple Crumble - $</label>150
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Cat Donut - $</label>150
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="150$">
    <label for="Davechoice">Cat Cupcake - $</label>150
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="200$">
    <label for="Davechoice">Frozen Yogurt - $</label>200
    <input type="number" value="1" min="1">
  </div>
  
  
   <h3> Meal Deals</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="1600$">
    <label for="Velmachoice">A Purrr-fect Lunch- $</label>1600
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="2500$">
    <label for="Davechoice">The BTS- $</label>2500
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="5000$">
    <label for="Davechoice">The Tabby Snack- $</label>5000
    <input type="number" value="1" min="1">
  </div>

   
  <h3>Cat Tuccino Specials</h3>
 
   <div>
    <input type="checkbox" id="Davechoice" value="1600$">
    <label for="Davechoice">10- Cat Tuccinos - $</label>1600
    <input type="number" value="1" min="1">
  </div>

   <div>
    <input type="checkbox" id="Davechoice" value="2500$">
    <label for="Davechoice">20- Cat Tuccinos - $</label>2500
    <input type="number" value="1" min="1">
  </div>

   <div>
    <input type="checkbox" id="Davechoice" value="3500$">
    <label for="Davechoice">30- Cat Tuccinos - $</label>3500
    <input type="number" value="1" min="1">
  </div>

   <div>
    <input type="checkbox" id="Davechoice" value="4500$">
    <label for="Davechoice">40- Cat Tuccinos - $</label>4500
    <input type="number" value="1" min="1">
  </div>

   <div>
    <input type="checkbox" id="Davechoice" value="5500$">
    <label for="Davechoice">50- Cat Tuccinos - $</label>5500
    <input type="number" value="1" min="1">
  </div>

   <div>
    <input type="checkbox" id="Davechoice" value="9000$">
    <label for="Davechoice">100- Cat Tuccinos - $</label>9000
    <input type="number" value="1" min="1">
  </div>

<h3>Fruit Explosion Special</h3>

   <div>
    <input type="checkbox" id="Davechoice" value="4500$">
    <label for="Davechoice">32- Fruit Explosions - $</label>4500
    <input type="number" value="1" min="1">
  </div>

   <h3>Special Events</h3>
   <div>
    <input type="checkbox" id="Davechoice" value="5000$">
    <label for="Davechoice">Small Event - $</label>5000
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="10000$">
    <label for="Davechoice">Medium Event - $</label>10000
    <input type="number" value="1" min="1">
  </div>
 
  <div>
    <input type="checkbox" id="Davechoice" value="20000$">
    <label for="Davechoice">Big Event - $</label>20000
    <input type="number" value="1" min="1">
  </div>

  <h3>Mystery Gifts</h3>

  <div>
    <input type="checkbox" id="Davechoice" value="1500$">
    <label for="Davechoice">1 Box - $</label>1500
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="4500$">
    <label for="Davechoice">3 Boxes - $</label>4500
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="6000$">
    <label for="Davechoice">5 Boxes - $</label>6000
    <input type="number" value="1" min="1">
  </div>

  
    
  

<div style="margin-bottom: 10px;"></div>
  
  <h3> Discount Items</h3> 

<div>
  <input type="checkbox" id="50off" value="-40%">
  <label for="50off">Employee Discount - 40% off</label>
  <input type="number" value="1" min="1" max="1">
</div>

<div>
  <input type="checkbox" id="30off" value="-30%">
  <label for="30off">PD & EMS - 30% off</label>
  <input type="number" value="1" min="1" max="1">
</div>

<div>
  <input type="checkbox" id="25off" value="-15%">
  <label for="25off">Mechs - 15% off</label>
  <input type="number" value="1" min="1" max="1">
</div>

<h3> Delivery </h3>
  
  <div>
    <input type="checkbox" id="ColinChoice" value="1000"><!--The price is the value, change that and then the name and itll change on the menu-->
    <label for="ColinChoice">Delivery Fee - $</label>1000
    <input type="number" value="1" min="1">
  </div>
  

  
  <div style="margin-bottom: 25px;"></div>


<div>
    <label for="name">Cashier's Name:</label>
    <input type="text" id="name">
  </div>
  

<div style="margin-bottom: 25px;"></div>
 
<div class="total-box">
  <span>Total: $</span>
  <span id="total">0.00</span>
</div>

<div class="total-box">
  <span>Commission (15%): $</span>
  <span id="discount-total">0.00</span>
</div>




 
  
  
  <div style="margin-bottom: 45px;"></div>
