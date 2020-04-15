Clipped from: https://stackoverflow.com/questions/7755088/what-does-href-expression-a-href-javascript-a-do



## What does href expression 

## <a href="javascript:;"></a> 

## do?



An `` element is invalid HTML unless it has either an `href` or `name` attribute. 

If you want it to render correctly as a link (ie underlined, hand pointer, etc), then it will only do so if it has a `href` attribute.

Code like this is therefore sometimes used as a way of making a link, but without having to provide an actual URL in the `href` attribute. The developer obviously wanted the link itself not to do anything, and this was the easiest way he knew.

He probably has some javascript event code elsewhere which is triggered when the link is clicked, and that will be what he wants to actually happen, but he wants it to look like a normal `` tag link.

Some developers use `href='#'` for the same purpose, but this causes the browser to jump to the top of the page, which may not be wanted. And he couldn't simply leave the href blank, because `href=''` is a link back to the current page (ie it causes a page refresh).

There are ways around these things. Using an empty bit of Javascript code in the `href` is one of them, and although it isn't the best solution, it does work.