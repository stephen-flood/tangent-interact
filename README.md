<!-- PART 1: Setup Scripts -->
<script src="https://sagecell.sagemath.org/static/jquery.min.js"></script>
<script src="https://sagecell.sagemath.org/embedded_sagecell.js"></script>
<script>
function makeAccessable(){document.querySelectorAll('.compute').forEach(function(b){var d=b.dataset.alt||"Interactive mathematical graphic.";b.querySelectorAll('img').forEach(function(i){i.alt=d});b.querySelectorAll('pre.sagecell_stdout').forEach(function(p){p.setAttribute('role','status');p.setAttribute('aria-label','Current values from the interactive')})})}
$(function(){sagecell.makeSagecell({inputLocation:'div.compute',template:sagecell.templates.minimal,evalButtonText:'Launch the Interactive Applet Now'});makeAccessable();new MutationObserver(makeAccessable).observe(document.body,{childList:true,subtree:true})});
</script>

<!-- PART 2: Descriptive Content -->
# Visualizing Tangent Lines

### Overview
- It is hard to define the slope for a function that is not a line. 
- A tangent line is the *line appoximating $f(x)$* at a single numerical value of $x$, called $a$.   
- We know from algebra how to find and interpret the slope of this *line*.

This interactive lets you move the graph of a tangent along a function, and see what the the changing tangent line tells us about the original function. 

### Instructions
- Use the slider to choose a value of $a$.
- The image displays the graph of $f(x)$, the point $(a,f(a))$, and the tangent line at that point.
- As you move the slider, watch use the slope ofthe the tangent *line* to describe the the non-linear funciton. 

<!-- PART 3: Sage Code -->
<div class="compute" 
            data-alt="The image shows the graph of a function and its tangent line at the selected point.">
<script type="text/x-sage">

f(x) = x^2 - 1
xmin = -2
xmax =  2
ymin = -2
ymax =  2

@interact 
def plot_tangent( a = slider( xmin, xmax, 0.05, -1.5 )):

    x1 = round(a,2)
    print(f"You have selected a = {x1}")

    p1 = plot( f(x) , x, (xmin,xmax) )

    fprime = derivative(f, x)
    y1 = f( x1 )
    m = fprime( x1 )
    tangentline(x) = m*(x - x1) + y1

    p2 = plot( tangentline(x), x, (xmin,xmax), ymin=ymin, ymax = ymax , color="red")

    p3 = point((x1, y1), size=30, color='black')

    show(p1+p2+p3)

    print("The tangent line is", end=" ")
    if m<0:
        print("going down, so the slope is negative.")
    elif m>0:
        print("going up, so the slope is positive.")
    else:
        print("flat, so the slope is zero.")
    
    print()

    print("Note: The point happens to be", end = " ")
    if y1 < 0:
        print("below the x-axis.")
    elif y1 > 0:
        print("above the x-axis.")
    else:
        print("on the x-axis." )
    print("But the height of the y-value is NOT relevant to the slope of the line.")

</script>
</div>
