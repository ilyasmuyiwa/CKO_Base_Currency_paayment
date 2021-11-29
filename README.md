# CKO_Base_Currency_paayment
Make payment from multiple currencies using the base currency
To install, go to ```vendor/checkoutcom/magento2/Controller/Payment/PlaceOrder.php``` and replace   ```$order->getOrderCurrencyCode()``` with ```$order->getBaseCurrencyCode()``` at around line 275

Then at fine ```vendor/checkoutcom/magento2/Model/Service/TransactionHandlerService.php``` line 475 in ```public function amountFromGateway($amount, $order = null)```

Add  

```$baseToOrderRate = $order ? $order->getBaseToOrderRate() : $this->order->getBaseToOrderRate();```

```$amount = $amount * $baseToOrderRate;```

Also ```vendor/checkoutcom/magento2/Model/Service/QuoteHandlerService.php```,
     line 300, in  ```public function amountToGateway($amount, $quote)``` 
 
Add

```$amount = $amount/$quote->getBaseToQuoteRate();```

``` $amount = round($amount, 2);```
       
       
And ```vendor/checkoutcom/magento2/Model/Service/OrderHandlerService.php``` line 202 
in method ```public function amountToGateway($amount, $order)``` 
        
Add 

```$amount = $amount/$order->getBaseToOrderRate();```

``` $amount = round($amount, 2);```
        
