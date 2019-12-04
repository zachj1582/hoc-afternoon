<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250" align="right">

# Project Summary

In this project, we'll practice creating a higher order component (HOC). This app will have the same general functionality as the app we will create in the sister project with a render prop. It is important to remember that these are two different patterns to accomplish the same task. In this project we will be building a currency converter that will convert a foreign currency to USD.

## Step 1

### Summary

In this step, we'll set up our file structure to keep things organized.

### Instructions

- Inside the `src` folder, create a `Components` folder.
- Open `src/Components`. Create two new Files:
  - CurrencyConverter.js
  - CurrencyDisplay.js

### Solution

<details>

<summary>File Structure</summary>

```
-- src
  -- Components
    -- CurrencyConverter.js
    -- CurrencyDisplay.js
  -- App.css
  -- App.js
  -- index.css
  -- index.js
```

</details>

## Step 2

### Summary

In this step, we'll create the skeleton for our Higher Order Component (HOC).

### Instructions

- Import React in `CurrencyConverter.js`.
- Create a function called `withCurrency` that will return a class component called `Currency`
- The `withCurrency` function should take one paramter we will call `BaseComponent`

<details>

<summary> Detailed Instructions </summary>

<br />

Remember, a Higher Order Component (HOC) is just a function that returns a new component. The naming convention of `withNAMEofFUNCTION` is common for HOC's.

We first want to create an arrow function called `withCurrency` that takes in one parameter, `BaseComponent`. The `withCurrency` function will return a new class-based component that we will call `Currency`

```js
const withCurrency = (BaseComponent) => (
  class Currency extends Component {...}
)
```

Give the returned `Currency` component a render method and have it return empty parentheses for now. This is where will put some JSX in a bit. The `BaseComponent` parameter will be used to hold the template of a component we will pass in once we invoke the function.

</details>

### Solution

<details>

<summary> <code> src/Components/CurrencyConverter.js </code> </summary>

```jsx
import React, {Component} from 'react'

const withCurrency = (BaseComponent) => (
  class Currency extends Component {
    render(){
      return (
        // soon to be jsx
      )
    }
  }
)
```

</details>

## Step 3

### Summary

In this step, we will create the boilerplate for our `CurrencyConverter`. This will include a drop down and buttons to increment and decrement the amount to convert.

### Instructions

- Set intial state for this component. We will need three keys: `currencyChosen : false`, `selectedCurrency: 'Select Currency'` and `amount: 0`.

```js
const currencyData = [
	{ name: 'Japanese Yen', symbol: '¥', rate: 113.6, id: 0 },
	{ name: 'British Pound', symbol: '£', rate: 0.77, id: 1 },
	{ name: 'Canadian Dollar', symbol: 'CAD', rate: 1.32, id: 2 },
	{ name: 'Mexican Peso', symbol: 'Mex$', rate: 20.41, id: 3 },
	{ name: 'Swiss Franc', symbol: 'Fr.', rate: 1.01, id: 4 }
]
```

- We will use the above array, `currencyData`, to map over and dynamically create options inside of a soon to be created `select` element.
- Create a `<select>` element to hold the options created above along with a single default option with a value of 'Select Currency'.
- Create two `<button>` elements, one should have `+` as it's inner text and the other should be `-`.
- Below the `button`'s display the `BaseComponent` parameter like it is a React Component.

<details>

<summary> Detailed Instructions </summary>

<br />

- Set some intial state for `Currency` component. We will need a `currencyChosen` which will default to `false`, `selectedCurrency` which will default as 'Select Currency' (spelling and capitalization are important here) and finally an `amount` with the default of `0`.

```js
const currencyData = [
	{ name: 'Japanese Yen', symbol: '¥', rate: 113.6, id: 0 },
	{ name: 'British Pound', symbol: '£', rate: 0.77, id: 1 },
	{ name: 'Canadian Dollar', symbol: 'CAD', rate: 1.32, id: 2 },
	{ name: 'Mexican Peso', symbol: 'Mex$', rate: 20.41, id: 3 },
	{ name: 'Swiss Franc', symbol: 'Fr.', rate: 1.01, id: 4 }
]
```

- Copy the above `currencyData` array inside of thhe `render()` method but outside of the `return` inside of the `Currency` component.
- Using `.map()`, create an `<option>` element for each item of the `currencyData` array. Each `<option>` element should have a `key` set to a unique value on the currency object (use the `id`), and `value` set to the `index` the currency occupies in the array, and have the individual currency name as text. Call the new array `currencyOptions`.
- Create a container div `<div>`. Inside of the `div` create a `<select>` element. Set its `value` equal to the `selectedCurrency` on state.
- Inside of the `select` create a single `<option>` element with a attribute of `value='Select Currency'` and 'Select Curreny' as the inner text. Below that, inside of `{}` display the `currencyOptions`.
- Create a new `<div>` to hold buttons that will increment and decrement the currency amount.
- Inside of the newly created `div`, create two `<button>` elements, one should have `+` as it's inner text and the other should be `-`. The button with the `+` should have a className of `add` and the button with the `-` should have a className of `minus`
- Below the `button`'s display the `BaseComponent` parameter like it is a React Component. The `BaseComponent` will have two props; one called `currency` which will use `selectedCurrency` from state as the index to select an option from the `currencyData` array and the other prop will be called `amount` which will be the value of amount on state.
  </details>

### Solution

<details>

<summary> <code> src/Components/CurrencyConverter.js </code> </summary>

```jsx
import React, { Component } from 'react'

const withCurrency = (BaseComponent) =>
	class Currency extends Component {
		state = {
			currencyChosen: false,
			selectedCurrency: 'Select Currency',
			amount: 0
		}

		render() {
			const currencyData = [
				{ name: 'Japanese Yen', symbol: '¥', rate: 113.6, id: 0 },
				{ name: 'British Pound', symbol: '£', rate: 0.77, id: 1 },
				{ name: 'Canadian Dollar', symbol: 'CAD', rate: 1.32, id: 2 },
				{ name: 'Mexican Peso', symbol: 'Mex$', rate: 20.41, id: 3 },
				{ name: 'Swiss Franc', symbol: 'Fr.', rate: 1.01, id: 4 }
			]
			const currencyOptions = currencyData.map((currency, index) => (
				<option key={currency.id} value={index}>
					{currency.name}
				</option>
			))
			return (
				<div>
					<select value={this.state.selectedCurrency}>
						<option value='Select Currency'>Select Currency</option>
						{currencyOptions}
					</select>
					<div>
						<button className='add'>+</button>
						<button className='minus'>-</button>
					</div>
					<BaseComponent
						currency={currencyData[this.state.selectedCurrency]}
						amount={this.state.amount}
					/>
				</div>
			)
		}
	}
```

</details>

## Step 4

### Summary

In this step, we'll create three methods to help us handle user interactions. We will be using the auto-binding (public class field syntax for these methods).

### Instructions

- Using the public class field syntax, create a method that will increment the count of amount on state. Use `setState` via the callback function syntax. Call this method `handleAmountIncrease`.
- Using the public class field syntax, create a method that will decrement the count of amount on state. Use `setState` via the callback function syntax. Call this method `handleAmountDecrease`.
- Using the public class field syntax, create a method that will handle the users selection from the dropdown. You will need to store their selection in a variable we will call `userValue`. Call this method `handleOptionSelect`.

<details>

<summary> Detailed Instructions </summary>

<br />

- Let's start off by creating a method that will handle the increase of the amount on state. We will be using the public class field syntax and using `setState` with a callback, rather than a object. The callback will take one parameter, `prevState`. This parameter gives us access to state without modifying it directly (this is an example of closure!). The callback function needs to return an object that will be used to update state.

```jsx
handleAmountIncrease = () => {
	this.setState((prevState) => {
		return {
			amount: prevState.amount + 1
		}
	})
}
```

- Next we will create a method that will handle the decrease of the amount on state. We will be using the public class field syntax and using `setState` with a callback for this as well. The callback will take one parameter, `prevState`. This parameter gives us access to state without modifying it directly.

```jsx
handleAmountDecrease = () => {
	this.setState((prevState) => {
		return {
			amount: prevState.amount - 1
		}
	})
}
```

- Finally we will create a method that will handle the user selection from the dropdown. We will be using the public class field syntax and using `setState` with a callback for this as well. This method will expect an event (`evt`) as it's only parameter. We will assign the value from `evt.target.value` to a variable we will call `userValue`. Return a new object from `setState` that updates `selectedCurrency` and `curencyChosen` on state. The new value of `selectedCurrency` will be the `userValue` variable. The new value of `currencyChosen` will be a boolean. Using a ternary, determine if `userValue` is equal to 'Selected Currency' (capitalization matters here). If it does, set the value to `false`, otherwise set to `true`.

```jsx
handleOptionSelect = (evt) => {
	const userValue = evt.target.value
	this.setState(() => {
		return {
			selectedCurrency: userValue,
			currencyChosen: userValue === 'Select Currency' ? false : true
		}
	})
}
```

- Last step is to use these methods in the appropriate spots.
  - Using an `onClick` event listener, use the `handleAmountIncrease` method on the button with a `+` as the inner text.
  - Using an `onClick` event listener, use the `handleAmountDecrease` method on the button with a `-` as the inner text.
  - Using an `onChange` event listener, use the `handleOptionSelect` method on the select element.

</details>

### Solution

<details>

<summary> <code> src/Components/CurrencyConverter.js </code> </summary>

```jsx
import React, { Component } from 'react'

const withCurrency = (BaseComponent) =>
	class Currency extends Component {
		state = {
			currencyChosen: false,
			selectedCurrency: 'Select Currency',
			amount: 0
		}

		handleAmountIncrease = () => {
			this.setState((prevState) => {
				return {
					amount: prevState.amount + 1
				}
			})
		}

		handleAmountDecrease = () => {
			this.setState((prevState) => {
				return {
					amount: prevState.amount - 1
				}
			})
		}

		handleOptionSelect = (evt) => {
			const userValue = evt.target.value
			this.setState(() => {
				return {
					selectedCurrency: userValue,
					currencyChosen: userValue === 'Select Currency' ? false : true
				}
			})
		}

		render() {
			const currencyData = [
				{ name: 'Japanese Yen', symbol: '¥', rate: 113.6, id: 0 },
				{ name: 'British Pound', symbol: '£', rate: 0.77, id: 1 },
				{ name: 'Canadian Dollar', symbol: 'CAD', rate: 1.32, id: 2 },
				{ name: 'Mexican Peso', symbol: 'Mex$', rate: 20.41, id: 3 },
				{ name: 'Swiss Franc', symbol: 'Fr.', rate: 1.01, id: 4 }
			]
			const currencyOptions = currencyData.map((currency, index) => (
				<option key={currency.id} value={index}>
					{currency.name}
				</option>
			))
			return (
				<div>
					<select
						value={this.state.selectedCurrency}
						onChange={this.handleOptionSelect}>
						<option value='Select Currency'>Select Currency</option>
						{currencyOptions}
					</select>
					<div>
						<button className='add' onClick={this.handleAmountIncrease}>
							+
						</button>
						<button className='minus' onClick={this.handleAmountDecrease}>
							-
						</button>
					</div>
					<BaseComponent
						currency={currencyData[this.state.selectedCurrency]}
						amount={this.state.amount}
					/>
				</div>
			)
		}
	}
```

</details>

## Step 5

### Summary

In this step, we'll invoke our function and build out a component to display the currency.

### Instructions

- At the bottom of the file, create a new variable called `ExchangedCurrency` which will hold the component returned from invoking `withCurrency`.
- One thing to remember is that `withCurrency` required a parameter we called `BaseComponent`. Since we will be invoking the `withCurrency` function, we need to create a component to use.
- Create a new component inside `CurrencyDisplay.js`. This component will be a functional component, meaning it has no state. We will need to have `props` be one of our parameters. Think back to the previous step, what were the two props on BaseComponent? You can destructure them if you want. We will use data from `props.currency` and the amount from `props.amount` to display and convert our currency.

<details>

<summary> <code> Detailed Instructions </code> </summary>

<br />

- At the bottom of `CurrencyConverter.js` create a new constant called `ExchangedCurrency`. This variable will hold the result of invoking `withCurrency`. Because `withCurrency` requires a `BaseComponent` parameter, we will need to create that but first we will need to export our `ExchangedCurrency` variable. (Part 1)
- Switch to our `CurrencyDisplay.js` file. This is where we'll display our converted currency. The component should be functional, take in one paramater called `props` and return some JSX. The JSX will be a `<p></p>` element. The `p` element should show the US Dollar amount, the name of the currency, the symbol and then the amount of the exchanged currency. Export the newly created component.
- Back inside of `CurrencyConverter.js`, import our `CurrencyDisplay.js` component and pass it as argument to the invocation of `withCurrency` at the bottom of the file. (Part 2)

</details>

### Solution

<details>

<summary> <code> src/Components/CurrencyConverter.js </code> Part 1 </summary>

```jsx
import React, { Component } from 'react'

const withCurrency = (BaseComponent) =>
	class Currency extends Component {
		// PREVIOUS STEPS
	}

const ExchangedCurrency = withCurrency()

export default ExchangedCurrency
```

</details>

<details>

<summary> <code> src/Components/CurrencyDisplay.js </code> </summary>

```jsx
import React from 'react'

const CurrencyDisplay = (props) => (
	<p>
		US Dollar ${props.amount.toFixed(2)} - {props.currency.name}{' '}
		{props.currency.symbol}
		{(props.amount * props.currency.rate).toFixed(2)}
	</p>
)

export default CurrencyDisplay
```

</details>

<details>

<summary> <code> src/Components/CurrencyConverter.js </code> Part 2 </summary>

```jsx
import React, { Component } from 'react'
import CurrencyDisplay from './CurrencyDisplay'

const withCurrency = (BaseComponent) =>
	class Currency extends Component {
		// PREVIOUS STEPS
	}

const ExchangedCurrency = withCurrency(CurrencyDisplay)

export default ExchangedCurrency
```

</details>

## Step 6

### Summary

In this step we need to import our newly created `ExchangedCurrency` component into `App.js`.

### Instructions

- Open `App.js`. Remove all of the existing code from Create React App and import `ExchangedCurrency` from `./Components/CurrencyConverter.js`.
- Render the component onto the screen but use a fragment rather than a div as it's parent container. Feel free to add an `h2` element above to signal that this is a Higher Order Component. In the next project you will create a Render Prop version of this same project and the heading will help you know which one is which.

### Solution

<details>

<summary> <code> src/App.js </code> </summary>

```jsx
import React, { Component } from 'react'
import './App.css'

import ExchangedCurrency from './Components/CurrencyConverter'

class App extends Component {
  render() {
    return (
      <>
        <h2>Higher Order Component</h2>
        <ExchangedCurrency />
      </>
    )
  }
}

export default App
```

</details>

## Step 7

### Summary

You may have noticed by now that our project doesn't run yet and we are getting an error `Cannot read name of undefined`. Think for a moment about what may be causing this problem?

This is happening because we are trying to display our `CurrencyDisplay.js` component before we have anything on our `currency` prop. In this step we will conditionally render text if the user hasn't selected an option from the dropdown.

### Instructions

- Inside of `CurrencyConverter.js`, look to the return statement and find where we are rendering the `BaseComponent`. We will need to conditionally render this component only if a user has selected something from the dropdown. If the user has not, we will display the text `Please Select Currency`.

<details>

<summary> Detailed Instructions </summary>

<br />

Head down to the return of the `Currency` component inside of `withCurrency`. Here we will use a ternary to determine if our user has selected something from the dropdownn. Luckily on state we have a key of `currencyChosen` which is a boolean. Use this to determine if we should display the BaseComponent or if we should display the text `Please Select Currency`.

</details>

### Solution

<details>

<summary> <code> src/Components/CurrencyConverter.js </code> </summary>

```jsx
import React, { Component } from 'react'
import CurrencyDisplay from './CurrencyDisplay'

const withCurrency = (BaseComponent) =>
	class Currency extends Component {
		state = {
			currencyChosen: false,
			selectedCurrency: 'Select Currency',
			amount: 0
		}

		handleOptionSelect = (evt) => {
			const userValue = evt.target.value
			this.setState(() => {
				return {
					selectedCurrency: userValue,
					currencyChosen: userValue === 'Select Currency' ? false : true
				}
			})
		}
    // OTHER STEPS
		render() {
      // OTHER STEPS
			return (
				<div>
          {/*OTHER STEPS*/}
					{this.state.currencyChosen ? (
						<BaseComponent
							currency={currencyData[this.state.selectedCurrency]}
							amount={this.state.amount}
						/>
					) : (
						<p>Please Select Currency</p>
					)}
				</div>
			)
		}
	}

const ExchangedCurrency = withCurrency(CurrencyDisplay)

export default ExchangedCurrency

```

</details>

## Black Diamond ◆

### Summary

This step is meant to stretch what you know and combine your knowledge. The first part of the black diamond is to make it so the user cannot go lower than 0. The second part of the challenge is to disable the buttons until an option from the dropdown has been selected.

The final challenge of the black diamond is to make it so every time a user selects a new currency it outputs a new currency display card rather than updating the same card each time.

## Contributions

If you see a problem or a typo, please fork, make the necessary changes, and create a pull request so we can review your changes and merge them into the master repo and branch.

## Copyright

© DevMountain LLC, 2017. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.

<p align="center">
<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250">
</p>
