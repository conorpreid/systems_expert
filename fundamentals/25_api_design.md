# API Design

### Some terms before beginning
- Pagination
  - Some network requests can nessesitate a large response
  - In these cases, the API serving the request can deliver a single page of results
  - And include an index to say "this is page 1 of X, ask if you want more"
  - Often used for List endpoints (think "trending YouTube Videos")
  - One would say the API response is Paginated
- CRUD Operations
  - Create, Read, Update, Delete
  - Bedrock of a functioning system and at the core of many API's

# Getting into it
API design is a sibling, not subset of Systems Design
Any product or service, there is an API that back that service
Might be multiple, its at the core of the product
Its bascially how they are built
Think Stripe - AlgoExpert use the Stripe API to process payments
Stripe API is bascially their product
There is an element of permenance to API's
  - As soon as people start using it, its very difficult to change
  - So, designing the API is extremely important
  - Lots of reviews/challenges happen at this stage

Typical question would be "Design Twitter" / "Design Stripe"
You then question + clarify
Typically it might "Design the Stripe API"
Then...what part? Who will consume?

Note: you can check out real world API's
Like [Stripe](https://stripe.com/docs/api/charges/object)
