# Shop Project Notes

Sometimes a deeply nested child component needs access to state that lives higher up in the component tree. One way to give it access is to pass the state down through each intermediate component as a prop until it reaches the child.

This technically gets the job done, but it creates a lot of prop drilling, which adds boilerplate and can slow down development. There are two primary solutions to this:

#### Solutions:
- Component Composition
- React Context API

Component composition means restructuring the components so that the part that needs access to the state is moved closer to where the state lives, often by passing it as a child or slot instead of drilling props through several layers.

### Example Context API Component
```tsx
import { createContext } from "react";

const ShoppingCartContext = createContext({
items:[]
});

export default ShoppingCartContext;
```
The context can store any value, text, object etc.
The above code creates the context

##### React return statement containing context being provided to components inside
```tsx
return (
<ShoppingCartContext.Provider value={shoppingCart}>
	<Header
	cart={shoppingCart}
	onUpdateCartItemQuantity={handleUpdateCartItemQuantity}
	/>
	<Shop onAddItemToCart={handleAddItemToCart}>
	{DUMMY_PRODUCTS.map((product) => (
	<li key={product.id}>
		<Product {...product} onAddToCart={handleAddItemToCart} />
		</li>
		))}
	</Shop>
</ShoppingCartContext.Provider>
);
```
As you can see above, it is wrapped in the context name with a .Provider at the end and the value to be put as context is provided as `value`

##### Accessing context
```tsx
import { use, useContext } from "react";

const cartCtx = use(ShoppingCartContext);
// or
const cartCtx = useContext(ShoppingCartContext);
```
