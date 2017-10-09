# Basic Flexblox Layout

## Flex layout 
1. To use flex layout, you should use this in the parent div:

        display:flex
        # you can also use inline-flex;

2. Terminology:
    - main axis : The main axis is the axis running in the direction the flex items are being laid out in.
    - cross axis : The cross axis is the axis running perpendicular to the direction the flex items are being laid out in. 
    - flex container : The parent element that has display: flex set on it is called the flex container.
    - flex items : The items being laid out as flexible boxes inside the flex container are called flex items.

3. Change the main axis:

        flex-direction: column
        # by default this is set to row.

4. Wrapping:

        # when you have a fixed amount of width or height in your layout is that eventually your flexbox children will overflow their container, breaking the layout. You can use this:
        flex-wrap: wrap

        # You can use flex-wrap to change both direction and wrap
        flex-flow: row wrap

5. Flex shortcut:    
>flex is a shorthand property that can specify up to three different values:    
- flex-grow : The unitless proportion value that dictates how much of the available space along the main axis each flex item will take up. 
- flex-shrink : This specifies how much of the overflowing amount is taken away from each flex item's size, to stop them overflowing their container. 
- flex-basis :  The minimum size value inside the flex value.    
- Most time we just use flex-grow and flex-basis.

## flex alignment
1. Horizontal alignment (main axis alignment):   
>justify-content controls where the flex items sit on the main axis. It define in the flex container    
- flex-start : The default value is flex-start, which makes all the items sit at the start of the main axis.
- flex-end : sit at the end.
- space-around :  It distributes all the items evenly along the main axis, with a bit of space left at either end.
- space-between : It is very similar to space-around except that it doesn't have any space at either end.

2. Vertical alignment (cross axis alignment):
>align-items controls where the flex items sit on the cross axis. It define in the flex container. And you can overwrite it for individual flex items by applying the align-self property to them.    
- stretch : If the parent hasn't got a fixed width in the cross axis direction, then all flex items will become as long as the longest flex items. 
- center : The center value that we used in our above code causes the items to maintain their intrinsic dimensions, but be centered along the cross axis. 
- flex-start : align all items at the start.
- flex-end : align all items at the end.