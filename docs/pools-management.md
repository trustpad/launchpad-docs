# How to setup sale pools

## IDO Pool

To setup a new sale, you need to create a new pool file in the `pools` directory, fill it in and include it in
the `pools/index.ts` file. That's it!

You will need some information from another project, let's take PenguinKarts project as an example:

```
- Date for the IDO? 25.02.2022
- Do you need KYC? No
- How many tokens for sale? 5,000,000
- Token price ($)? 0,04
- What chain are you launching on? Fantom (FTM)
- Token name? Penguin Karts
- Token symbol? PGK
- Token decimals? 18
- Token initial supply (at TGE)? 117,657
- Token total supply? 200,000,000
- What's the token vesting schedule? 10% 30 min. after TGE - 1 Month cliff, Thereafter 5 months linear
- When do you plan to list? TGE at 23-03-2022
```

Here's the step-by-step guide:

1. Copy the `pools/_template.tsx` file and paste it as `pools/penguinKarts.tsx`
2. Open the copied file
3. Change the exported variable name from `tokenId` to `penguinKarts`. This is how thew new pool will be exported
4. Then change the pool properties in the object:
   1. `id` to `penguinKarts`. This ID is used in URLs and many other places
   2. `kyc`: depends on whether you want people to KYC for this sale
5. Now fill in the sale info in the `sale` nested object:
   1. `tokensForSale`: how much is sold. For the example above: `toWeiBN(5_000_000)`
   2. `startDate`: ISO-formatted date of sale start. `2022-02-25T11:00:00.000Z`
   3. `rate`: amount of tokens for each unit of `fundToken`, so `rate = 1 / tokenPrice`. For the example
      above: `rate = 1 / 0.04 = 25`
   4. `durationHours`: how long is the sale duration
6. Now fill in the token information:
   1. `chain`: BSC, ETH, DOT, SOL, ADA, POLY, etc
   2. `address`: can be filled when you know the address and want to make it public for people
   3. `name`: token name
   4. `symbol`: token symbol
   5. `imageSrc`: token image. You need to put the image in the same directory or `images` sub-directory and import it
      in the pool config file
   6. `listingTime`: ISO-formatted listing time
   7. `initialSupply`: available tokens at TGE
   8. `totalSupply`: total tokens supply
7. Add project social links in the `social` object
8. Specify the project description in `description`
9. Optionally, use `descriptionShort` if you want to have a long `description` on the pool page, but short on the pool
   card
10. Finally, import that file in the `pools/index.ts` like `import { penguinKarts } from './penguinKarts.tsx'` and add
    the `penguinKarts` variable in the list of pools

After that the sale should appear on the website.

## Deploy it

Once the pool is setup, you need to deploy the sale to be able to open the registration. It is more convenient to run the project locally, so you don't wait for the pool config to be deployed before deploying it.

1. Go to the admin page
2. Choose the newly added sale in the selector
3. Press "Deploy", wait
4. Press "Prepare"
5. Copy the new address and paste it in the pool `sale.address` property
6. Now you can deploy the new sale and manage its config in the admin panel: registration timeline, duration, total tokens, etc


## INO Pool

TODO