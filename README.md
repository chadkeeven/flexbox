# CSS Box Model and Positioning: Flexbox Model

## Objectives
After this lesson, students will be able to:
- Describe how the Flexbox model differs from the regular CSS Box Model
- Name the basic properties that compose the Flexbox structure
- Explain a scenario in which Flexbox would be useful
- Create a simple layout using only Flexbox properties

## Preparation
- Before this lesson, students should already be able to:
- Write basic CSS
- Write basic HTML
- Use the chrome console
- Use the CSS box model to create simple layouts

## Living Box Model - Round 1

Before we start in on Flexbox, let's recap the CSS box model. It's main properties are:

- Display
- Float
- Clear
- Position
- Margin
- Padding*
- Border*

To make sure we still remember these, we're going to act them out. Half of the class will get a pad of post-its to write CSS properties on, and the other half has to act them out.
> Note - Padding and Border might be hard to act out. Let's stick with the first 5 properties.

If you have post-its, take two of them and write one CSS property/value on each. Hand each of your two post-its to a different person.

## Why Flexbox?
So by now (hopefully) everyone is familiar with the CSS box model. But perhaps while constructing your last page layout, you noticed some of the flaws in the available tools - clearing and floating alone is enough of a headache to modern developers that many people working in the field have trouble describing how it works.

That's one reason why the Flexbox Model was created - its a more logical layout model that was added to the CSS3 spec in order to streamline page structuring, using CSS properties that match more common layout needs.

Flexbox is so new that [it just recently obtained full browser support](http://caniuse.com/#search=flexbox)soon, it  may start to replace the CSS box model as the dominant tool for page structure. So it is for sure a great tool to learn!

## An Intro to The Flexbox Model
The Flexbox Model is a series of CSS rules that affect the two main components of a web layout - the parent container, and the child elements. This is a structure we're already familiar with from past lessons - a block-level element is created as a "container", and holds inside of it a list of smaller elements:

```html
	<ul class="flex-container">
		<li id="item-1" class="flex-item">1</li>
		<li id="item-2" class="flex-item">2</li>
		<li id="item-3" class="flex-item">3</li>
		<li id="item-4" class="flex-item">4</li>
		<li id="item-5" class="flex-item">5</li>
		<li id="item-6" class="flex-item">6</li>
	</ul>
```
By default, the CSS Box Model allows you to control your child elements as a list - they can be arranged only in the order they appear in the DOM. With the Flexbox Model, you'll be able to rearrange your child elements along a grid, in any direction and order you wish, sorted either forward or backwards. 
In the above code, our unordered list `flex-container` is holding a collection of list items we'd like to arrange. From here, there's a number of CSS properties that we can apply to either our container or our children.

## Box Model Demo 

Let's write some HTML we can come back to and use to visualize what we're talking about.

1. Create an new directory called flexbox-practice (or fork this repo)
2. Create html page called index.html with an externally linked css stylesheet called main.css
3. Inside your html page create a "flex-container" `ul` holding six list items within, with each next node numbered.

Your HTML should look something like this:

```html
	<html>
	<!DOCTYPE html>
	<html>
	<head>
		<title>Flexbox Practice</title>
		<link rel="stylesheet" type="text/css" href="main.css">
	</head>
	<body>
		<ul class="flex-container">
		  	<li id="child-1" class="flex-item">1</li>
		  	<li id="child-2" class="flex-item">2</li>
		 	<li id="child-3" class="flex-item">3</li>
		  	<li id="child-4" class="flex-item">4</li>
		  	<li id="child-5" class="flex-item">5</li>
		  	<li id="child-6" class="flex-item">6</li>
		</ul>
	</body>
	</html>
</html>
```
4. Let's also add some basic styles to reset our list and list items:

```css
ul {
	list-style: none;
	margin: 0;
	padding: 0;
}
ul li {
	padding: 14px;
	font-size: 2em;
	border: 1px solid #000;
}
```
## The Flexbox Model and its components

As we've discussed, the Flexbox Model has two main components - the parent element, and the children. Let's break down the Flexbox properties based on which object they're meant for:

### Properties of the Parent
First, let's take a look at the CSS calls we can use to shape the parent container:

#### Display
This one should be familiar - only the value of the property is new:
```css
.flex-container {
	display: flex;
}
```
This call denotes that our parent - and everything inside it - will be using the Flexbox Model. Just declaring this is enough to turn our layout into a very basic Flexbox layout - but probably not with any of the customization we want. This call has to be made before any of the following Flexbox properties can be used. 
> Note - `display: flex` gives your element Flexbox properties, but will allow it to be treated as a block-level element by all the other elements it share the page with. If you'd like your parent element to mimic the display properties of an inline element, use `display: inline-flex`. 

Go ahead and add `display: flex;` to our `.flex-container`.

#### Flex-Direction
Flex-direction determines how our child elements will lay out inside their parent:

```css
.flex-container {
	flex-direction: row;
}
```
- **row (default)**: left to right 
- **row-reverse**: right to left
- **column**: top to bottom
- **column-reverse**: bottom to top

Set `.flex-container` to be `flex-direction: row`.

### Flex-Wrap

By default, children in your Flexbox layout will all try to fit on one line. You can also tell items to wrap, or wrap in reverse order:

```css
.flex-container {
	flex-wrap: wrap;
}
```
- **nowrap (default)**: single-line, left to right
- **wrap**: multi-line, left to right 
- **wrap-reverse**: multi-line, right to left

Set our `.flex-container` to be `flex-wrap: wrap`.

### Properties of the Children

Next, let's take a look at the CSS calls we can use to arrange our child elements:

### Order

Just like the CSS Box Model, our child elements are laid out in the order the DOM receives them. But unlike the CSS Box Model, we can change that order with CSS:

```css
#child-1 {
	order: 2;
}
```

By default, all children are `order: 1`. When multiple items have the same order number, they're called in the order the DOM receives them. Since the order property is unit-less and the values can be stacked, we can use the order property arrange properties into sets, completely reorder them, and any sequence inbetween. The above CSS arranges our first child element to actually appear at the end of the list - after any elements with a default 1 value, but before elements with an order value higher than 2.

Let's take minute to rearrange the order of our child elements:

- Make `#child-1` have an order value of 3.
- Make `#child-2` have an order value of 2.
- Make `#child-3` have an order value of 1.
- Leave the other children in the order the DOM recieves them in.

Open your `index.html` file in Chrome - notice how the elements now appear out of order? Or rather, in the order we told them to? This is the magic of Flexbox!

![magic](gifs/magic.gif)

### Flex-Grow

If we want certain elements to take up a larger amount of space than another, we can achieve this with flex-grow:

```css
 #child-1 {
  flex-grow: 2;
}
```

Like Order, `flex-grow` is unit-less - meaning that `flex-grow: 2` will make `#child-1` twice as large as all other elements. Once again, the default value is 1. 

Take a minute to resize our child elements:

- Make `#child-1` have a `flex-grow` value of 2.
- Make `#child-3` have an `flex-grow` value of 3.
- Leave the other children at their default size.

Refresh `index.html` and see how our elements fill the page now - they strech to fill their container, while maintining a consistent size!

### Responsive Flexibility

Grab your browser window by the corner, and squish your screen (or use the mobile/responsive emulator in the Chrome Dev Tools) until it's roughly the size of an iPad, or smartphone - see how the boxes squish proportionally as the screen becomes smaller? What happens when the screen get too small to display all of the boxes on a single line? Can you remember what property is responsible for that action?

## Living Box Model - Round 2

Now that we've learned two different layout models, let's combine them!
In the begining of class, half the class was handed a pad of post its to write CSS properties on, and the other half had to act them out. This time, we'll have two stacks of post-its - one for CSS Box Model, and one for Flexbox Model. Please perform whatever role you didn't perform last round.

## Column Flow - Paired Practice 

In your career as a web developer, you'll almost always be asked to work with large datasets. As you gain the skills to sort and classify these data points behind the scenes with tools like Javascript, you'll also need to know how to show users these datasets in ways that are both meaningful and familiar to them. This often comes in the form of building layouts based on websites your clients are familiar with, or are widely popular.
One such example is Pinterest, which did a lot to kick-off the wide-spread adoption of column-based, endless scrolling, tiled-based layouts:

[Pinterest](https://www.pinterest.com/)

This type of layout might have been intimidating only a few minutes ago - but now that we know flexbox, you might have a better idea of how to arrange this layout.

Open the folder called pinterestPractice - inside, you'll find an HTML file populated with an assortment of cat photos. You'll also see a (mostly) blank CSS file attached - work with a partner to recreate the layout you see on Pinterest.com.

Things to consider:

1. What can you do to make sure that the Flexbox children fill the full width and height of a row, but don't stretch the images?
2. What Flexbox properties can you use to adjust for gaps caused by the differently-shaped pictures? Hint- there's a pattern to the image sizes. 
3. How does your grid look at different screen sizes? Is it responsive? If not, what can you do to make sure it is?

##### Bonus:
4. Check out Mozilla's overview of the [Flexbox Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)
In the left menu, under Properties, you'll see a full list of Flexbox CSS properties. See if any ones we haven't touched on yet can help you build a better grid.

You'll be given the remainder of class to create your best Pinterest Grid, after which each pair will showcase their prototype, and the style rules they used to achieve it.

## Conclusion

So now we have two different ways of laying out content on our sites - they can be used separately or combined in order to achieve the kind of pages we want.

![Room for Activities](gifs/activities.gif)

To recap:

1. How are children treated differently in the Flexbox Model? What are few abilities they gain?
2. What are some of the Flexbox properties? What's the bare minimum amount of properties you can use to still have a Flexbox layout?
3. How would adding clears and floats affect your Flexbox layout?
4. What kind of situation might be a bad fit for using the Flexbox Model?







