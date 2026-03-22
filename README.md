<!-- BEGIN Setup Scripts -->
<script src="https://sagecell.sagemath.org/static/jquery.min.js"></script>
<script src="https://sagecell.sagemath.org/embedded_sagecell.js"></script>
<script>
  $(function () {
// Make *any* div with class 'compute' a Sage cell
// From sage for undergraduates
sagecell.makeSagecell({inputLocation: 'div.compute',
            template:       sagecell.templates.minimal,
                       evalButtonText: 'Launch the Interactive Applet Now'});
});
</script>
<script>
function applySageAlt() {
  document.querySelectorAll('.compute').forEach(function (box) {
    box.querySelectorAll('img').forEach(function (img) {
      img.alt = box.dataset.alt || "Interactive mathematical graphic.";
    });
  });
}
$(function () {
  sagecell.makeSagecell({
    inputLocation: 'div.compute',
    template: sagecell.templates.minimal,
    evalButtonText: 'Launch the Interactive Applet Now',
    callback: function () {
      applySageAlt();
      new MutationObserver(applySageAlt).observe(document.body, {
        childList: true,
        subtree: true
      });
    }
  });
});
</script>
<!-- END Setup Scripts  -->


# Webpage Title

## Overview

(Explain the mathematics here)

## Instructions

(Explain how to use your interactive here)


<div class="compute" 
            data-alt="Graph of y = x^2 - 1 with the region between a and b shaded.">
<script type="text/x-sage">

f(x) = x^2 -1

@interact
def myIntegralPlot( a = slider(-2, 2, 0.05, -1.5 ), b = slider(-2, 2, 0.05, 1 ) ):
    epsilon = 10^-12
    
    # this takes care of several different drawing issues
    # whenever b < a, or in other words, the bounds are backwards.
    left_bound = min( a, b )
    right_bound = max( a, b )
    
    # the 10^-12 in the next line might surprise you, but it is because the
    # program reacted badly when both a=1 and b=1.
    P1 = plot( f(x), x, left_bound, right_bound + epsilon, fill=True )
    P2 = plot( f(x), x, -2, 2, gridlines='minor', ymin=-2, ymax=3)
    P3 = text("$\\int_a^b ( x^2 - 1 ) \\; dx$", (0, -1.75), fontsize=24 )
    
    # this colored arrow avoids student confusion when bounds are backwards
    if (a < b):
        P4 = arrow( (-0.5, 0.99), (0.5, 1), color='green' )
        P = P4 + P1 + P2 + P3
    elif (b < a):
        P4 = arrow( (0.5, 1), (-0.5, 0.99), color='red' )
        P = P4 + P1 + P2 + P3
    else:
        # note, this is for the a=b case
        P = P1 + P2 + P3
    
    
    P.show()
    
    print()
    print("Final Value Roughly ", N( integral( f(x), x, a, b) ))
    
    return

</script>
</div>
