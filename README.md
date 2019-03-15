# Nifty-markets-transactions

Updated Transactions Documentation

## OVERVIEW ## 

These endpoints are going to be extremely similar, almost the exact same as the wishlist. You should even be able copy and paste a lot of code, and just change wishlist to transactions in many places. Transaction IDs work just like Wishlist IDs, in that a person's first transaction may actually be transactionId 47, for example.


### GET Users Transactions ###

URL: /api/users/:id/transactions

Example return from /api/users/1/transactions:

```
[
    {
        "transactionId": 1,
        "buyer": "scott",
        "buyerId": 1,
        "seller": "lauren",
        "sellerId": 20,
        "itemId": 1,
        "name": "Love Ranger",
        "price": 10,
        "description": "Aim for the heart.",
        "img_url": "https://cdn.thetrackernetwork.com/cdn/fortnite/93062_large.png",
        "availability": 1
    },
    {
        "transactionId": 2,
        "buyer": "scott",
        "buyerId": 1,
        "seller": "john",
        "sellerId": 10,
        "itemId": 20,
        "name": "Magikarp",
        "price": 1,
        "description": "Utterly useless",
        "img_url": "https://cdn.bulbagarden.net/upload/0/02/129Magikarp.png",
        "availability": 0
    }
]
```


## GET Users Transaction by Transaction ID ##

URL: /api/users/:id/transasctions/:transactionId

NOTE: notice there is no 's' in `transactionId`

Example return from /api/users/1/transactions/1

```
{
    "transactionId": 1,
    "buyer": "scott",
    "buyerId": 1,
    "seller": "lauren",
    "sellerId": 20,
    "itemId": 1,
    "name": "Love Ranger",
    "price": 10,
    "description": "Aim for the heart.",
    "img_url": "https://cdn.thetrackernetwork.com/cdn/fortnite/93062_large.png",
    "availability": 1
}
```

## POST Transaction to Transaction List ##

This is where the fun begins. Here, the front end hardly has to do with updating state, the POST will do it all. When a POST is made, the transaction is recorded, noting who the buyer and the seller are, and for what price. After the POST is done, the buyer and seller will both have a new transaction on their transaction list, with all the details of the transaction. Also, the item will be automatically updated, giving the item a new `userId` and `username` of the buyer, as well as setting the availability to false.

URL: /api/users/:id/transactions

Example POST, user 1 (scott) will buy item 19 from quinn:

```
{
	"buyerId": 1,
	"sellerId": 9,     //---This is equivelant to the userId on the item.
	"itemId": 19
}
```

If successfully, you will receive a success message, along with a `newTransactionsList`. Example:

```
{
    "message": "Congratulations on your new purchase!",
    "newTransactionsList": [
        {
            "transactionId": 3,
            "buyerId": 1,
            "sellerId": 9,
            "itemId": 19,
            "transaction_type": null
        }
    ]
}
```

## DELETE Transaction from Transaction List ##

I imagine this would only be used for testing, but it's available if needed.

URL: /api/users/:id/:transactionId


If successfully, you will receive a success message, along with a `newTransactionsList`. Example:

```
{
    "message": "Transaction removed from transactions list",
    "newTransactionsList": [
        {
            "transactionId": 1,
            "buyerId": 1,
            "sellerId": 20,
            "itemId": 1,
        },
        {
            "transactionId": 2,
            "buyerId": 1,
            "sellerId": 10,
            "itemId": 20,
        }
    ]
}
```
