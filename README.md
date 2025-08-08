# mongodb

<details>
<summary>Return all paid orders which was placed (created) 10 minutes ago</summary>

```js
const tenMinutes = 10;

const orders = await orders.aggregate([
  { $match: { state: OrderState.PAID } },
  { $addFields: { ordersCreatedTenSecondsAgo: { $add: ['$createdAt', tenMinutes * 60 * 1000] } } },
  { $match: { ordersCreatedTenSecondsAgo: { $lt: new Date() } } },
  { $project: { _id: 1 } },
])
```

</details>

<details>
<summary>Return documents where a field (let's say the field is called myField) is a string with length greater than 0</summary>

```js
user.find({
  middleName: {
    $type: "string",
    $ne: ""
  }
})
```

</details>

<details>
<summary>Fetch all products where their profile configuration has a price tag which is some kinda of special offer</summary>
<table><thead><tr><th>Table Schema</th><th>Query</th></tr></thead>
<tbody><tr><td>

```ts
interface Product {
  _id: ObjectId,
  profile: {
    config: {
      priceTags: [
        {
          specialOffer: [
            {
              expiresAt: Date,
              // ...
            }
          ]
        }
      ]
    }
  }
}
```

</td><td>

```js
product.find({
  "profile.config.priceTags": {
    $elemMatch: {
      "specialOffer.0": { $exists: true }
    }
  }
})
```

</td></tr></tbody></table>
</details>
