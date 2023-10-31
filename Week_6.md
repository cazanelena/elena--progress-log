## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/full-stack-app/learning-outcomes/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.
> **[Learning outcome...]**
> Like everyone else that tried to use next js 13 and react probably bumped into the error: "You can use client components on the server components".

> Server components can import and render client components, but client components can't render the server components in it. If you want to use a server component in a client component we user Context API in React to manage the state and make it global.
**> Code below:**

```js
"use client";

import { createContext, useReducer } from "react";

const initialBasket = {
  articles: [],
};

const reducer = (state, action) => {
  switch (action.type) {
    case "ADD":
      return { ...state, articles: [...state.articles, action.article] };
    case "REMOVE":
      return { ...state, articles: state.articles.filter(article => article["name"] != action.articleName) };
    case "RESET":
      return {articles: [] };
    default:
      return state;
  }
};

export const BasketContext = createContext({ state: initialBasket, dispatch: () => null });

export const BasketContextProvider = ({
  children,
}) => {
  const [state, dispatch] = useReducer(reducer, initialBasket);

  return (
    <BasketContext.Provider value={{ state, dispatch }}>
      {children}
    </BasketContext.Provider>
  );
};
```

 ### 2. Show an example of a learning outcome you have struggled with and/or would like to re-visit.
> [**Learning outcome...**]  
After we maganed to make the shopping cart working we realized that we don't want to have our button on the home page but instead we wanted to move it to the item route where we could see all the other details such a color, size,description.
> Trying to make this work was a bit more complicated because of the way we written our code. We decided instead of manageing the state in a function that dispaly the items we will move it only to the button. So we made a btn component and pass in the item as a prop.
> We ended up having a few bugs and struggling to debug it. The item we were passing through as a prop it was undefined.
Here is the btn to add item to the basket. Prop is 'product'.
```js

export const Add_item_basket = ({product}) => {
    const { dispatch } = useContext(BasketContext);


    const addToBasket = (product) => {
        dispatch({ type: 'ADD', article: product });
      };

    return (
        <>
        <button key={uuidv4()} onClick={() => addToBasket(product)}>Add to basket</button>
        </>
    )
}
```
Here we pass it through each product route:

```js
<ul className="variants">
            {allVariants.map((variant) => (
              <li key={variant.colour}>
                <Link href={`/products/${params.id}/${variant.id}`}>
                  {variant.colour}
                </Link>
              </li>
            ))}
          </ul>
          <Add_item_basket selectedProduct={selectedProduct} />
        </>
      ) : (
        <div>
          <Image
            src={selectedProduct.image}
            alt={selectedProduct.name}
            width={200}
            height={100}
          />
          <p>Colour: {selectedProduct.colour}</p>
          <Add_item_basket selectedProduct={selectedProduct} />
          <Link href={'/basket'}>Basket</Link>
        </div>
```
Instead of ``` <Add_item_basket selectedProduct={selectedProduct} />``` we should have be consistent with our props naming and keep it ``` <Add_item_basket product={selectedProduct} />```
Lesson learned. Can't wait to start using TypeScript!!!

## Feedback
### Alphonso's feedback
#### What Went Well
More than anything else, I like your enthusiasm for TypeScript! I'm a fan of it 👌
This is a pretty comprehensive delve into your use of a Reducer, it's clearly been a really useful learning experiment :) 

#### Even Better If
These are small things, but I think it's worth keeping these habits in mind, specially this early on in your journey:

Be mindful of readability. As a codebase grows (imagining this project were picked up later on and more features were added) it gets exponentially harder to read.
Think of how your code reads to human eyes as it grows.
Here I'm making the assumption that these actions refer to Articles in your basket. But you could well add functionality to your page to allow users to list new Artciles for sale. The handle 'ADD' would then need to be replaced everywhere on the code.
```javascript
const reducer = (state, action) => {
  switch (action.type) {
    case "ADD":
      return { ...state, articles: [...state.articles, action.article] };
    case "REMOVE":
      return { ...state, articles: state.articles.filter(article => article["name"] != action.articleName) };
    case "RESET":
      return {articles: [] };
    default:
      return state;
  }
};
```

This is pretty much nitpicking, but you're rendering just a button in the snippet below. You don't need to wrap it in anything.
```javascript
    return (
        <>
        <button key={uuidv4()} onClick={() => addToBasket(product)}>Add to basket</button>
        </>
    )
```
