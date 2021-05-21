# Stripe Integration
---

author: #anzal 

---

### Which stripe integration is best for Indian Merchants?
- Stripe Save and Reuse
	- This method save cards for future payments

Reference: https://stripe.com/docs/payments/save-and-reuse?platform=web	


## Integration details
### UI
1. Add or choose a card
![[Pasted image 20210521154316.png]]
Here's the style used: [[styling stripe]]

Requirements: 
- `client_secret` - we get this by creating an intent to setup a card. Check 'backend' section below for details

```html

<div class="ui  ">

  <div class="sr-root">
    <div class="sr-main">
      <%if(saved_cards&&saved_cards.length>0){%>
      <div class="ui segments">
        <% saved_cards.forEach(function(card){%>
          <form class="ui form segment" method="POST" action="/api/{{estimate_for_payment_id}}/payment/stripe/pay_with_stripe_payment_method">
            <div class="ui ">
              <b>
              <%=_.capitalize(card.card.brand) %> <%=_.capitalize(card.card.funding)%> Card </b> ending in <%=card.card.last4%> expires on <%=card.card.exp_month%>/<%=card.card.exp_year%>
            </div>

            <button class="ui   green button " type="submit" style="float: right;">Pay</button>
            <br>
            <br>
            <input name="payment_method_id" value="<%=card.id%>" hidden>
          </form>
          <%}) %>
      </div>
      <div class="ui horizontal divider">OR</div>
      <%}else{%>
        <br>
        <div class="ui segment">
          <span>You don't have any saved cards</span>
          <br>  </div>

        <br>

      <%}%>
      <form id="setup-form" data-secret="<%=client_secret%>" >
        <h3>Link a new card</h3>
        <!-- <div class="sr-form-row">
          <label>
            Account details
          </label>
          <input type="text" id="email" placeholder="name" />
        </div> -->
        <input type="text" id="email" placeholder="Email address" style="border-color: white;"  />

        <div class="sr-form-row">
          <label>

          </label>
          <!-- <div class="sr-input sr-element sr-card-element" id="card-element"> -->
          <div class="" id="card-element" style="background-color: white;padding:1em;">
            <!-- A Stripe card Element will be inserted here. -->
          </div>
        </div>
        <div class="sr-field-error" id="card-errors" role="alert"></div>
        <button id="submit" class="ui basic blue fluid button">
          <div class="spinner hidden" id="spinner"></div>
          <span id="button-text">Link your card to your account</span>
        </button>
      </form>

      <form class="ui new_card_created form segment" method="POST" action="/api/{{estimate_for_payment_id}}/payment/stripe/pay_with_stripe_payment_method<%=(req.url.search('new_user_pay')!=-1)?'?new_user_pay=true':''%>" style="display: none;">
        <input name="payment_method_id" id="new_card_payment_id" value="" hidden>
      </form>
      <div class="sr-result hidden">
        <p>Card setup completed<br /></p>

      </div>
    </div>
  </div>
</div>





<script src="https://js.stripe.com/v3/"></script>
<script>
   $('.button[type="submit"]').click(function(){
          $(this).addClass('loading');
          $(this).addClass('disabled');
    })

  var stripe = Stripe('<%=sails.config.stripe.pk_secret%>');


  // Element styles
  var elements = stripe.elements();
  var card = elements.create('card');
  card.mount('#card-element');

  
  // Handle payment submission when user clicks the pay button.
  var button = document.getElementById("submit");
  button.addEventListener("click", function(event) {
    event.preventDefault();
    changeLoadingState(true);
    var email = document.getElementById("email").value;

    stripe
      .confirmCardSetup('<%=client_secret%>',
      {
        payment_method: {
          card: card,
          billing_details: { email: email }
        }
      })
      .then(function(result) {
        console.log(result)
        if (result.error) {
          changeLoadingState(false);
          var displayError = document.getElementById("card-errors");
          displayError.textContent = result.error.message;
        } else {
          // The PaymentMethod was successfully set up
          orderComplete(stripe, '<%=client_secret%>');
        }
      });
  });




// Show a spinner on payment submission
var changeLoadingState = function(isLoading) {
  if (isLoading) {
    document.querySelector("button").disabled = true;
    document.querySelector("#spinner").classList.remove("hidden");
    document.querySelector("#button-text").classList.add("hidden");
  } else {
    document.querySelector("button").disabled = false;
    document.querySelector("#spinner").classList.add("hidden");
    document.querySelector("#button-text").classList.remove("hidden");
  }
};

/* Shows a success / error message when the payment is complete */
var orderComplete = function(stripe, clientSecret) {
  stripe.retrieveSetupIntent(clientSecret).then(function(result) {
    var setupIntent = result.setupIntent;
    var setupIntentJson = JSON.stringify(setupIntent, null, 2);


    document.querySelector(".sr-result").classList.remove("hidden");

    setTimeout(function() {
      document.querySelector(".sr-result").classList.add("expand");
    }, 200);

    changeLoadingState(false);
    $('#new_card_payment_id').val(setupIntent.payment_method)
    $('.new_card_created').submit()
  });
};


</script>

```

### Backend
1. Create customer and store
```
stripe.customers.create({
  name: org.owner.name,
  email: org.owner.email,
  address: {
	line1: `${org.name},${org.country}`,
	country: `${sails.config.countries.find(country => country.name == org.country).code || 'US'}`,
  }
}).then(function (customer) {
  var org_details = org.details || {}
  _.set(org_details, 'thirdparty_accounts.stripe_customer', customer)
  Org.updateOne({ id: org.id }).set({ details: org_details }).exec(function (err, org) { })
  callback(null, customer)
})
```

2. Create card setup intent
Use this when customer wants to setup a new card
```
  stripe.setupIntents.create({
	customer: results.findOrgCreateStripeCustomer.id,
  }).then(function (intent) {
	callback(null, intent)
  })
```

3. Fetch saved cards
```
  stripe.paymentMethods.list({
	customer: results.findOrgCreateStripeCustomer.id,
	type: 'card',
  }).then(function (saved_cards) {
	callback(null, saved_cards)
  })
```


4. Charge a saved card
```
stripe.paymentIntents.create({
	amount: amount,
	currency: currency,
	customer: results.findOrgCreateStripeCustomer.id,
	payment_method: payment_method_id,
	off_session: true, //this lets you charge without customer being on session
	confirm: true,
	description: 'VA service',
  }).then(function (intent) {
	if (intent.status == 'succeeded') {
			res.redirect(`/api/v1/estimate/${estimate.id}/payment/stripe/capture_saved_card_payment?intent_id=${intent.id}`)

	} else {
	  console.log(results)
	  res.send('payment failed')
	}
  })
```


5. Authorize payment received
Fetch the payment intent and confirm if the payment is received
```
async function authorizeStripePaymentIntentAndGetPaymentDetails(paymentIntentID, callback) {
  if (!paymentIntentID) return callback(new Error("Invalid params, 'paymentIntentID' is mandatory"));
  const pg_response = await stripe.paymentIntents.retrieve(paymentIntentID);
  if (!pg_response || _.isEmpty(pg_response)) {
    callback(new Error(`Payment Details not found for sessionID: ${paymentIntentID}`));
  } else if (pg_response.status != 'succeeded') {
    callback(pg_response.status);
  } else {
    //paid
    callback(null, pg_response);
  }

}
```