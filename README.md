## Website Performance Optimization portfolio project

This is project 4 of Udacity Frontend Web Nano Degree project. The objective is to optimize this online portfolio for speed. In particular, optimize the critical rendering path and make this page render as quickly as possible. The original files for this project is located at the [Udacity's GitHub Repository for Mobile Portfolio](https://github.com/udacity/frontend-nanodegree-mobile-portfolio)<br>
The goals are:
* Optimize index.html to achieve page score of 90 or higher.
* Modify main.js for pizza web site so the time to resize pissas is less than 5 ms.
* Modify main.js for pizza web site so the frame rate when scrolling is 60 fps.

### How to run 

#### Option 1. Locally on your desktop

1. Check out the repository
1. Double click index.html to open the portfolio project on your browser. You cannot measure the page speed this way. See the next section to setup a local web server and expose it to the internet.
1. To see the pizza's website, from the portfolio page, click on the link to Cam's Pizzeria. Open the console in the develooper tool to see the output of different timers.

#### Option 2. Setup a local web server using python and expose it to the internet
Follow the instructions cut and pasted from the instructors for this class:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights to see the page score. [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)
1. To see the pizza's website, from the portfolio page, click on the link to Cam's Pizzeria. Open the console in the developer tool to see the output of different timers.

### List of optimizations done for this project

#### Optimization of index.html to achieve page score of 90 or higher.

What I did to optimize the index.html page:
* Took out the link to google fonts to eliminate network request. The link also did not have http on it, so it took a very long time for the page to load since it couldn't find it.
* Added the reference to the font faces directly as inline CSS.
* For print.css, I added media=print so it is only requested during print.
* The call to google analytic javascript file and script can be loaded asynchronously so it will not parse blocking. Added "asynch" in the tags.
* I modified the style.css by combining multiple definitions to save character bytes. I also changed a couple references such as footer span to a class, since it's simpler and less costly.
* Since the style.css is pretty small, I put everything as an inline CSS to eliminate network request.
* I created a 100 px image for the pizzeria thumbnail and compressed it.
* I minified index.html. The development's version will be index-dev.html.

#### Modification of main.js so the time to resize pizzas is less than 5 ms

I changed changePizzaSizes(size) function:
* changed all selectors of .querySelector or .querySelectorAll to either getElementById or getElementsbyClassName since they are faster
* put the result of most of the selector to a variable outside the loop so the selector does not have to get run again and again. For example: I created the variable pizzaLength to get document.getElementsByClassName("randomPizzaContainer").length
* took out all the variables that do not have to be inside the loop outside the loop so they are not repeated for each pizza.
* took out all the functions that do not have to be run inside the loop outside. 

I took out sizeSwitcher(size) function from determineDx(size) as a stand alone function. This function only needs to be run once to find the new size outside the loop in the changePizzaSizes(size) function.

DetermineDx(size) function is not used:
* To calculate the new width per pizza, we just need to find what the new size should be, either 0.25, 0.3333, or 0.5 relative to the window width. We do not need to loop
  through to find out what is the current width and add it back on. This is a simple calculation that does not need function, just assign the result to a variable called newwidth outside the loop.


#### Modification of main.js to get frame rate of 60 fps while scrolling

I modified the the DOMContentLoaded function in the add event listener:
* changed .querySelector to getElementById for movingpizza1. This is only need to be done once, so I moved it outside the loop.
* since there are only 5 phases for 8 columns, we do not need to load 200 objects at once. 40 should be enough. I changed the quantifier in the for loop from 200 to 40.

I modified the updatePositions() function:
* there are only 5 unique phases, so we do not need to calculate the phase for each 40 objects. I created an array called phases for those 5 unique phases.
* the body's scrolltop just need to be found once, so I moved that into a variable outside the loop.

### Resources Used
All resources that I used are in the Resources-Lists.txt

### Student's Info
Siska Ko<br>
siska.ko@gmail.com

### Resources Cut and Pasted from the Instructor:

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

#### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

#### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

#### Sample Portfolios

Feeling uninspired by the portfolio? Here's a list of cool portfolios I found after a few minutes of Googling.

* <a href="http://www.reddit.com/r/webdev/comments/280qkr/would_anybody_like_to_post_their_portfolio_site/">A great discussion about portfolios on reddit</a>
* <a href="http://ianlunn.co.uk/">http://ianlunn.co.uk/</a>
* <a href="http://www.adhamdannaway.com/portfolio">http://www.adhamdannaway.com/portfolio</a>
* <a href="http://www.timboelaars.nl/">http://www.timboelaars.nl/</a>
* <a href="http://futoryan.prosite.com/">http://futoryan.prosite.com/</a>
* <a href="http://playonpixels.prosite.com/21591/projects">http://playonpixels.prosite.com/21591/projects</a>
* <a href="http://colintrenter.prosite.com/">http://colintrenter.prosite.com/</a>
* <a href="http://calebmorris.prosite.com/">http://calebmorris.prosite.com/</a>
* <a href="http://www.cullywright.com/">http://www.cullywright.com/</a>
* <a href="http://yourjustlucky.com/">http://yourjustlucky.com/</a>
* <a href="http://nicoledominguez.com/portfolio/">http://nicoledominguez.com/portfolio/</a>
* <a href="http://www.roxannecook.com/">http://www.roxannecook.com/</a>
* <a href="http://www.84colors.com/portfolio.html">http://www.84colors.com/portfolio.html</a>


