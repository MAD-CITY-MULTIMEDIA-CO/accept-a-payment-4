# Accept a payment with Stripe Checkout

This integration shows you how to accept payments with Stripe [Checkout](https://stripe.com/docs/checkout).

Building a payment form UI from scratch is difficult -- input field validation, error message handing, and localization are just a few things to think about when designing a simple checkout flow.

We built [Checkout](https://stripe.com/docs/payments/checkout) to do that work for you so now you can focus on building the best storefront experience for your customers.

Once your customer is ready to pay, use Stripe.js to redirect them to the URL of your Stripe hosted payment page. 🥳

## How to run locally

Recommended approach is to install with the [Stripe CLI](https://stripe.com/docs/stripe-cli#install):

```sh
stripe samples create accept-a-payment
```

Then pick:

```sh
prebuilt-checkout-page
```

This sample includes several different server implementations and several different client implementations. The servers all implement the same routes and the clients all work with the same server routes.

Pick a server:

- [dotnet](./server/dotnet)
- [go](./server/go)
- [java](./server/java)
- [node](./server/node)
- [node-typescript](./server/node-typescript)
- [php](./server/php)
- [python](./server/python)
- [ruby](./server/ruby)
- [php-slim](./server/php-slim)

Pick a client:

- [html](./client/html)
- [react-cra](./client/react-cra) (React with create-react-app)






**Installing and cloning manually**

If you do not want to use the Stripe CLI, you can manually clone and configure the sample yourself:

```
git clone https://github.com/stripe-samples/checkout-one-time-payments
```

Copy the .env.example file into a file named .env in the folder of the server you want to use. For example:

```
cp .env.example client-and-server/server/node/.env
```

You will need a Stripe account in order to run the demo. Once you set up your account, go to the Stripe [developer dashboard](https://stripe.com/docs/development#api-keys) to find your API keys.

```
STRIPE_PUBLISHABLE_KEY=<replace-with-your-publishable-key>
STRIPE_SECRET_KEY=<replace-with-your-secret-key>
```

The other environment variables are configurable:

`STATIC_DIR` tells the server where to the client files are located and does not need to be modified unless you move the server files.

`DOMAIN` is the domain of your website, where Checkout will redirect back to after the customer completes the payment on the Checkout page.

**2. Create a Price**

[![Required](https://img.shields.io/badge/REQUIRED-TRUE-ORANGE.svg)](https://shields.io/)


You can create Products and Prices in the Dashboard or with the API. This sample requires a Price to run. Once you've created a Price, and add its ID to your `.env`.

`PRICE` is the ID of a [Price](https://stripe.com/docs/api/prices/create) for your product. A Price has a unit amount and currency.


You can quickly create a Price with the Stripe CLI like so:

```sh
stripe prices create --unit-amount 500 --currency usd -d "product_data[name]=demo"
```

Which will return the json:

```json
{
  "id": "price_1Hh1ZeCZ6qsJgndJaX9fauRl",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1603841250,
  "currency": "usd",
  "livemode": false,
  "lookup_key": null,
  "metadata": {
  },
  "nickname": null,
  "product": "prod_IHalmba0p05ZKD",
  "recurring": null,
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "one_time",
  "unit_amount": 500,
  "unit_amount_decimal": "500"
}
```

Take the Price ID, in the example case `price_1Hh1ZeCZ6qsJgndJaX9fauRl`, and set the environment variable in `.env`:

```sh
PRICE=price_1Hh1ZeCZ6qsJgndJaX9fauRl
```

**3. Follow the server instructions on how to run**

Pick the server language you want and follow the instructions in the server folder README on how to run.

For example, if you want to run the Node server:

```
cd server/node # there's a README in this folder with instructions
npm install
npm start
```

If you're running the react client, then the sample will run in the browser at
`localhost:3000` otherwise visit `localhost:4242`.


**4. [Optional] Run a webhook locally**

You can use the Stripe CLI to easily spin up a local webhook.

First [install the CLI](https://stripe.com/docs/stripe-cli) and [link your Stripe account](https://stripe.com/docs/stripe-cli#link-account).

```
stripe listen --forward-to localhost:4242/webhook
```

The CLI will print a webhook secret key to the console. Set `STRIPE_WEBHOOK_SECRET` to this value in your `.env` file.

You should see events logged in the console where the CLI is running.

When you are ready to create a live webhook endpoint, follow our guide in the docs on [configuring a webhook endpoint in the dashboard](https://stripe.com/docs/webhooks/setup#configure-webhook-settings).

## FAQ

Q: Why did you pick these frameworks?

A: We chose the most minimal framework to convey the key Stripe calls and concepts you need to understand. These demos are meant as an educational tool that helps you roadmap how to integrate Stripe within your own system independent of the framework.

Q: What happened to Plans and SKUs?

A: Plans and SKUs were old ways to model recurring and one-off prices. We created the Prices API to unify the two concepts and make it easier to reason about your pricing catalog. You can still pass old Plan and SKU IDs to Checkout -- to learn more read [our docs](https://stripe.com/docs/payments/checkout/migrating-prices) but know that you do not need to migrate any of your existing SKUs and Plans.

## Get support
If you found a bug or want to suggest a new [feature/use case/sample], please [file an issue](../../issues).

If you have questions, comments, or need help with code, we're here to help:
- on [IRC via freenode](https://webchat.freenode.net/?channel=#stripe)
- on Twitter at [@StripeDev](https://twitter.com/StripeDev)
- on Stack Overflow at the [stripe-payments](https://stackoverflow.com/tags/stripe-payments/info) tag
- by [email](mailto:support+github@stripe.com)

Sign up to [stay updated with developer news](https://go.stripe.global/dev-digest).

## Author(s)

- [@adreyfus-stripe](https://twitter.com/adrind)
- [@thorsten-stripe](https://twitter.com/thorwebdev)
- [@cjavilla-stripe](https://twitter.com/cjav_dev)