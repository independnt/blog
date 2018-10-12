---
layout: post
title:      "React and styled components"
date:       2018-10-12 22:26:44 +0000
permalink:  react_and_styled_components
---


Recently i started to learn a bit about styled components, as opposed to the more traditional CSS, or other stylesheet languages like SASS. First off, why not just stick to CSS? Well, anyone who works with CSS can tell you about the CSS anarchy that can follow, let alone trying to add logic to your styles. Luckily, pre-processors give us helpful features and let us do things like assigning variables, or multiple assigning, but still, it could definitely be easier. So styled components is one of the libraries trying to help us make these specific issues, a thing of the past.

Your React preferences are your own, some use yarn, i myself am just accustomed to using npm, so in order to install styled components, simply enter the command:

```
npm install --save styled-components
```

BTW if you want to read more about styled components, or wish to use them youself, check out more ![here](hhttps://www.styled-components.com/docs/basics).

Anyways, styled components lets us focus on single use cases, which with something like React, gives us control over every component, and every detail within said components. For instance, one of the only things we can't handle with styled components is going to be the entirety of the background. If we want one singular background, then we would still need to handle that within App.css, but otherwise, we can handle it all within the component instelf. For instance, if i'm in App.js and i want to handle the padding for everything within App.js, i can create a variable like so:

```
const AppLayout = styled.div `
 padding: 30px;
`

#Now i can use AppLayout and put everything else within my newly created tag

<AppLayout>
 <h1>Welcome!</h1>
  <p>This is just an example</p>
</AppLayout>
```

Now everything within AppLayout will adhere to the css stylings i inserted in it's variable above. Pretty neat. Take it a step further and you can create another component within the layout which in this case, is a navbar:

```
const Bar = styled.div `
  margin-bottom: 30px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
`

<AppLayout>
 <Bar>
  <h1>Item</h1>
	<h1>Item</h1>
	<h1>Item</h1>
 </Bar>
</AppLayout>
```

Now everything within AppLayout adheres to it's style and anything within Bar will adhere to the style we entered. We're using CSS grid here so we use the fr unit (fraction) which will evenly display our items next to eachother with even space inbetween. So all h1's will now be at the style desired. The great thing is that we can also use javascript to integrate conditional styles. 

Let's say we're using this navbar and we want to have a logo, along with links that display a new color/size. We can create a Logo variable which is equal to a styled.div, and links as another styled.div:

```
const Logo = styled.div`
  font-size: 1.5em;
`

const LinkButton = styled.div `
  cursor: pointer;
`

<AppLayout>
 <Bar>
   <Logo>
	  Logo Example!
	 </Logo>
	 <LinkButton onClick={()=>{this.setState({page: 'Example One'})}}>
	  Example Number One
	 </LinkButton>
	 <LinkButton onClick={()=>{this.setState({page: 'Example Two'})}}>
	  Example Number two
	 </LinkButton>
 </Bar>
</AppLayout>
```

Now our Logo and LinkButton Adhere to the Bar custom div, which adheres to the AppLayout custom div and the Logo and LinkButtons have their own style as well. Much easier than having a bunch of div's with class names or id's! Now we can add an onClick handler which can change a state which will be set to the current link selected!

```
constructor(){
    super()
    this.state = {
      page: "Example One"
    }
  }

  displayingExampleOne = () => this.state.page === 'Example One'
  displayingExampleTwo = () => this.state.page === 'Example Two'
```

Here we have our state set by default to example one, and two functions that return booleans either true or false for the current state.page. Lastly, we can enter an 'active' prop on each LinkButton:

```
<LinkButton onClick={()=>{this.setState({page: 'Example One'})}} active={this.displayingExampleOne()}>
	  Example Number One
	 </LinkButton>
	 <LinkButton onClick={()=>{this.setState({page: 'Example Two'})}} active={this.displayingExampleTwo()}>
	  Example Number two
	 </LinkButton>
```

Now that our LinkButtons have an active prop that only allows for one to be true at a time, we can add our conditional, directly to the styled.div set to LinkButton:

```
const LinkButton = styled.div `
  cursor: pointer;
  ${props => props.active && css`
		font-size: 1.2 em;
  `}
`
```

Here, our conditional under cursor: pointer; is saying the same thing as 

```
${function(props){
 if(props.active){
  return font-size: 1.2 em;
 }
}
```

So we're saying if LinkButton's active prop (which is equal to a boolean) is true, then give us this styling. THis normally can be done with css using things like onHover and transition, but having everything within the component helps you keep your code organized and easy to manage. At least that's how i look at it! Styled components seems like something easy to learn, but difficult to master. So i'll keep learning, and hopefully keep writing about it. Thanks for reading!
