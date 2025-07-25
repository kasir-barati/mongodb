# mongodb

<details>
<summary>Fetch all products where their profile configuration has a price tag which is some kinda of special offer</summary>
<table><thead><tr><th>Table Schema</th><th>Query</th></tr></thead>
<tbody><tr>

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

<td></td>

<td>

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
