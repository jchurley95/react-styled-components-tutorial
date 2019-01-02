# React with Styled Components

### Before this tutorial, you should a basic understanding of the following:
- React
- State and props
- JSX
- CSS
- Ternary statements
- If you are not familiar with React: https://github.homedepot.com/jch4905/basic-react-tutorial
- If you are not familiar with CSS: https://www.w3schools.com/css/
- If you are not familiar with Ternary Statements, just if/else written differently (familiar === true ? "familiar" : "not familiar")

## What are styled components?
- An npm package (called styled-components)
- A dynamic way to style your app
- Component based, like React

```javascript
// Creating styled components
import styled from 'styled-components'

const PageWrapper = styled.div`
    text-align: center;
`
const PageTitle = styled.h1`
    color: #444444;
`
const PageDescription = styled.h3`
    color: ${props => props.firstDescription ? "gray" : "orange"};
`
```

```javascript
// implementing styled components in JSX
<PageWrapper>
    <PageTitle>Welcome to Styled Components</PageTitle>
    <PageDescription firstDescription={true}>Not Required</PageDescription>
    <PageDescription firstDescription={false}>But very useful</PageDescription>
</PageWrapper>
```

In a very basic sense, **styled components** are defined as variables and replace the names of our HTML elements (div, h1, button) within our JSX. You do not need to understand yet what is happening in the code above, it is just there to show a very basic example, and we will explain more about what is happening as we continue on with this tutorial.

## Why would I use styled components?
I personally believe that styled components help people with less modern front-end experience do a better job of styling react components. Here's a few reasons why.
### React is inherently component based
React and styled components are both component based and as a result are highly compatible with eachother. They work well together for creating re-usable code with dynamic styling in a "reacty" way.

### Styled components can receive props
They can easily change your styling as your component state and props update. When we implement a styled component, it gains access to the props of that JSX element.

```javascript
// Styled component reading the prop
const PageDescription = styled.h3`
    color: ${props => props.firstDescription ? "gray" : "orange"};
`
```

```javascript
// JSX passing prop
<PageDescription firstDescription={true}>Not Required</PageDescription>
<PageDescription firstDescription={false}>But very useful</PageDescription>
```

### Styled components just read better
This is an opinionated answer, but it really can help. On a team, you are always writing code for the next person. The big page or component that you just built might make perfect sense to you, but odds are you are not the only one who will end up working on that.

Picture a file filled with a sea of divs and other HTML elements, each with their own props and classNames that can change based on props or state and inline styling mixed in with some inline javascript that references values from state or props and conditional renderings based on state or prop values...even that sentence is a mess trying to fit all that in.

Alternatively, picture a well structured file with descriptive names for the JSX elements that do not require you to look further for a class or id, allowing you to quickly separate in your mind the structure, styling, and functionality of your component, and just focus on the changes that need to be made.

Using styled components and good, descriptive naming conventions, you can make your code so simple to read through that people who have never written code could potentially read and interpret your code. Again, this might not matter for you personally, but the next person who needs to work on this code might have less familiarity than you do with the code language/framework or even the English language, and this is something that you can do to help them do their job to the fullest.

### Conclusion
Styled components enhance the readability, flexibility, reusability, and separation of concerns within your code. They are a way for you to separate your JSX from your styling, while also separating out any ***styling changes** based on props. If you work on a team where code quality sometimes suffers due to a lack of overall experience with react or front-end in general, they can help your team members do a better job of interpreting the existing code, and then making well structured and meaningful changes.

## How do I use styled components?
While there is a correct way to create and implement styled components, it is up to you/your team to decide how and where to put them in your app. 
### Creating a styled component
Lets go back to the example we saw at the beginning.

```javascript
// Creating styled components
import styled from 'styled-components'

const PageWrapper = styled.div`
    text-align: center;
`
const PageTitle = styled.h1`
    color: #444444;
`
const PageDescription = styled.h3`
    color: ${props => props.firstDescription ? "gray" : "orange"};
`
```

First of all, because it is an external npm package, we have to import the package into our file. 
```javascript
import styled from 'styled-components'
```

Next, we need to create a styled component using the `styled` function that we imported. To create a div, you would make a `styled.div`. You can also create a `styled.button` or a `styled.input` or any other html element.
We set this equal to a variable, and then we have some odd looking syntax where we use a pair of backticks to enclose all our css that will associate with that styled component. These are called template literals. If you want to understand more about them, here is some further reading: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals

Once you have created a styled component, you can proceed to list any and all css values in there using the same naming conventions and rules as regular css.

```javascript
const PageWrapper = styled.div`
    text-align: center;
`
```

### Implementing a styled component
If you created the styled components in a separate file, you will need to export them from there and then import them into your file with your JSX. If you created them in the same file, then you can just go ahead and reference them instead of your normal HTML tags.

```javascript
// Without styled components
<div>
    <h1>Welcome to Styled Components</h1>
    <h3>Not Required</h3>
    <h3>But very useful</h3>
</div>
```

```javascript
// With styled components
<PageWrapper>
    <PageTitle>Welcome to Styled Components</PageTitle>
    <PageDescription>Not Required</PageDescription>
    <PageDescription>But very useful</PageDescription>
</PageWrapper>
```

### Passing props to styled components
Again, when we implement a styled component, it gains access to the props of that JSX element.

```javascript
// Creating styled components
const PageDescription = styled.h3`
    color: ${props => props.firstDescription ? "gray" : "orange"};
`
```

```javascript
// JSX with props
<PageDescription firstDescription={true}>Not Required</PageDescription>
<PageDescription firstDescription={false}>But very useful</PageDescription>
```

The `${}` syntax is another example of template literals, but just understand that in our case this syntax allows us to write some javascript that returns a value for the css property based on the props passed to the component. That ternary statement basically says if the prop of `firstDescription` is not false, null, undefined, or zero, then the font color inside that h3 will be `orange`, otherwise it will be `gray`.

This is a simple example that only really achieves avoiding a minor amount of repeat code, and the prop that it reads will never change. One of the main benefits of styled components is how well they respond to changing prop values.

For a better example, consider the Home Depot UX style guide. Most of the components listed there such as buttons and system alerts have different "states" they can be in, such as the `error, disabled, or warning` states. Each of these states has its own color theme (red for error, gray for disabled, yellow for warning). If the state of the component changes, the color theme needs to change as well. For this example, imagine that the component just receives its props of currentState from a parent component. Also, this is a very simplified version of the component.

```javascript
// UXButton.js
import styled from 'styled-components';

const UXButtonWrapper = styled.button`
    color: ${props => props.styling.color};
    background: ${props => props.styling.background};
    cursor: ${props => props.styling.cursor};
`

const getStylingBasedOnCurrentState = (currentState) => {
    let styling = {
        color: "#444444",
        background: "white",
        cursor: "pointer"
    }
    if (currentState === "error") {
        styling.color = "red"
        styling.background = "#FBCBCD"
        styled.cursor = "pointer"
    }
    else if (currentState === "disabled") {
        styling.color = "#666666"
        styling.background = "#999999"
        styling.cursor = "not-allowed"
    }
    return styling
}

const UXButton = (props) => {
    return (
        <UXButtonWrapper styling={getStylingBasedOnCurrentState(props.currentState)}>{props.buttonText}</UXButtonWrapper>
    )
}
```

Basically, we just take in a prop of currentState and use it set a prop of styling equal to the return value of our getStylingBasedOnCurrentState function, and then we make each css property in the styled component equal to props.styling.`whatever the current property is`

In the process, we also set things up in a way that is easy to write useful tests should we import the getStylingBasedOnCurrentState function into a test file.

### You can still create your "css" files with them
For housekeeping purposes, you should probably create your styled components in a separate file, export them, then import them where needed. This allows you to create instances of that shared styled component across your entire app, avoiding repeating yourself. Also, it makes your component file less crowded. I recommend doing this from the beginning rather than waiting for it to get crowded.

My team created our own naming convention for files containing the styled components of our apps. We decided on calling them ComponentName.styled.js, where the .styled does not actually mean anything and just allows the the file to stand out in our file tree like a ".css" file would for that component.

For this example, just move the logic and styling into their own file.
```javascript
// UXButton.styled.js
import styled from 'styled-components';

const UXButtonWrapper = styled.button`
    color: ${props => props.styling.color};
    background: ${props => props.styling.background};
    cursor: ${props => props.styling.cursor};
`

const getStylingBasedOnCurrentState = (currentState) => {
    let styling = {
        color: "#444444",
        background: "white",
        cursor: "pointer"
    }
    if (currentState === "error") {
        styling.color = "red"
        styling.background = "#FBCBCD"
        styled.cursor = "pointer"
    }
    else if (currentState === "disabled") {
        styling.color = "#666666"
        styling.background = "#999999"
        styling.cursor = "not-allowed"
    }
    return styling
}

export {
    UXButtonWrapper,
    getStylingBasedOnCurrentState
}
```

Then, import our styled component and function back into the component file.

```javascript
// UXButton.js
import {UXButtonWrapper, getStylingBasedOnCurrentState} from './UXButton.styled'

const UXButton = (props) => {
    return (
        <UXButtonWrapper styling={getStylingBasedOnCurrentState(props.currentState)}>{props.buttonText}</UXButtonWrapper>
    )
}
```

## Cool extra stuff
### You can extend them off of eachother
One cool way to avoid repeat code and make your app easier to maintain is extending styled components off of eachother. To show an example of this, we will look at another way we could have styled that UXButton component.

```javascript
// UXButton.styled.js
const UXButtonBaseStyle = styled.button`
    height: 50px;
    width: 100px;
`
const NormalButton = UXButtonBaseStyle.extend`
    color: #444;
    background: white;
`
const ErrorButton = UXButtonBaseStyle.extend`
    color: red;
    background: pink;
`
const WarningButton = UXButtonBaseStyle.extend`
    color: gray;
    background: yellow
`
const DisabledButton = UXButtonBaseStyle.extend`
    color: gray;
    background: different gray;
`

export {
    UXButtonBaseStyle,
    NormalButton,
    ErrorButton,
    WarningButton,
    DisabledButton
}
```

### Referring to other styled components
I have only ever found a couple times that this was useful, but it is a cool ability. The offical styled component docs can explain it better than I can:
https://www.styled-components.com/docs/advanced#referring-to-other-components

## Helpful tip
- I used to always name the main wrapper JSX using a naming convention of "ComponentNameContainer". If you were to look through a lot of the code I have written, you would see this. However, as someone pointed out, Container is sort of a reserved term for Redux Containers. Because of this, I now always use the word "Wrapper" instead of "Container".

#You're Done