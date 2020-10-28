Intro
This module allows you to add a field to the webform module to redirect submissions to a payment processor. It requires the Webform module.
It is currently setup to work with FastTransact for payment processing but should be modifiable to work with any post and redirect style payment system.
There is no admin interface for this module. You will need to modify the code for your payment page.

Installation
Besides the usual Drupal steps to enable this module, you will need to do the following inside of Drupal manually.

Create a new boolean field in your webform content type with machine name 'field_webform_payment'. On our site the label is set to 'Payment is involved'
but you can label as you like. The 'on value' is set to 'Yes' and the 'off value' should be set to 'No'. (Yes, we should add this to the module at some point..)
Modify the ibbr_payment.module file to the correct URLs for your payment page with fast transact. The default page used for redirect is: 'https://umd-ibbr-events.fasttransact.net/SingleSignOn.aspx'. You also need to set up the paymentcode being sent to FastTransact. The bursar gave us 212 as our payment code for events.
Your payment page on FastTransact needs to be setup to redirect successful payments to the location of the payment_recieved.php page. You need to setup a Flexfield on your payment. This will hold the webform submission ID.
Modify the payment_received.php file with your correct URLs. Lastly, you may modify the email being sent confirming payment.


Usage

Create a new webform and select 'Yes' on the boolean field you created at install.
Several default fields will be added to the webform. You may alter help text or other options but leave the machine names as listed! You may also add whatever other fields you need to the webform. e.g. Their phone number or dietary restrictions.

The payment options field has a particular format that must be used to properly get payment data for the processor. The safe key name actually does not matter here. The readable option should consist of text describing the option followed by the price with a space, the '$' and then the price as a decimal. For example: 
Option1| Registration $60
In this case there is only one payment option of $60 for registration.
Option 1| Single day (no dinner) $120Option2| Full event with dinner $250
In this case there are 2 payment options. You can add as many as you like.

When a user submits this webform, the 'Submit button' will be replaced by a button labeled 'Forward to payment processor'. Clicking this button saves their webform submission in the 'draft' state and sends them to the payment page. Upon successful payment they will be redirected back to a page you specify in the module code.

If the user leaves the payment page or hits the back button, a new submission will be submitted to Webform but saved as 'draft' only successful payments will be moved from the draft status. If you ever decide to manually authorize a payment for someone, a webform admin will have to alter this draft status in the webform manually as well.
