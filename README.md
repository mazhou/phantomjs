#
## install Cases
https://www.npmjs.com/package/phantom

sudo  -H npm install phantom --save


(命令行操作) 安装phantom http://phantomjs.org/download.html

vi ~/.bash_profile

alias phantomjs='~/PATH/*/phantomjs'

## Use Cases
<pre>
var phantom = require('phantom');

phantom.create().then(function(ph) {
	ph.createPage().then(function(page) {

		page.property("viewportSize", {'width': 200, 'height': 100});
		page.property("content",'《html》《body》《canvas id="surface" width="200" height="100"》《/canvas》《/body》《/html》');
                
                ⚠️
                需要把"《"转换为"<",把"》"转换为">"
		
		
                // page.content = '<html><body><canvas id="surface" width="200" height="100"></canvas></body></html>';
		
		page.evaluate(function() {
			var c=el = document.getElementById('surface');
			var ctx = el.getContext('2d');
			ctx.font="40px Verdana";
			var gradient=ctx.createLinearGradient(0,0,c.width,0);

			gradient.addColorStop("0","magenta");
			gradient.addColorStop("0.5","blue");
			gradient.addColorStop("1","red");

			//把他赋值给fillStyle

			ctx.fillStyle=gradient;

			ctx.fillText("1234wA",10,80);
		})

		page.render('2.png');

		setTimeout(function(){
			ph.exit();
		},1000);
	
	});
});







</pre>
<pre>
var phantom = require('phantom');
phantom.create().then(
	function(ph) {
	  	ph.createPage().then(function(page) {
	  		
	  		page.viewportSize = {
			  	width: 500,
			  	height: 400
			};

			page.open('http://localhost:8888/1.html').then(function(status) {
			// page.open('http://www.baidu.com/').then(function(status) {
				console.log(status);
				page.property('content').then(function(content) {
					// console.log(content);
		        	page.viewportSize = {
					  	width: 200,
					  	height: 100
					};
				  		
				  	page.clipRect = {
						top: 0,
						left: 0,
						width: 200,
						height: 100
					};

					page.paperSize = {
					  	width: '100px',
					  	height: '50in',
					  	margin: {
					    	top: '0px',
					    	left: '0px'
					  	}
					};
		   
					setTimeout(function () {
				       
				        page.render('1.png');
			        	page.close();
			        	ph.exit();

				        console.log('render ok');
				     }, 1000);
		        	
		      	});
		    });
		});
	}
);

</pre>


--------------------------------------------------------------------------------------

# [PhantomJS](http://phantomjs.org) - Scriptable Headless WebKit

PhantomJS ([phantomjs.org](http://phantomjs.org)) is a headless WebKit scriptable with JavaScript.  The latest [stable release](http://phantomjs.org/release-2.1.html) is version 2.1.

**Note**: Please **do not** create a GitHub pull request **without** reading the [Contribution Guide](https://github.com/ariya/phantomjs/blob/master/CONTRIBUTING.md) first. Failure to do so may result in the rejection of the pull request.

## Use Cases

- **Headless web testing**. Lightning-fast testing without the browser is now possible!
- **Page automation**. [Access and manipulate](http://phantomjs.org/page-automation.html) web pages with the standard DOM API, or with usual libraries like jQuery.
- **Screen capture**. Programmatically [capture web contents](http://phantomjs.org/screen-capture.html), including CSS, SVG and Canvas. Build server-side web graphics apps, from a screenshot service to a vector chart rasterizer.
- **Network monitoring**. Automate performance analysis, track [page loading](http://phantomjs.org/network-monitoring.html) and export as standard HAR format.

## Features

- **Multiplatform**, available on major operating systems: Windows, Mac OS X, Linux, and other Unices.
- **Fast and native implementation** of web standards: DOM, CSS, JavaScript, Canvas, and SVG. No emulation!
- **Pure headless (no X11) on Linux**, ideal for continuous integration systems. Also runs on Amazon EC2, Heroku, and Iron.io.
- **Easy to install**: [Download](http://phantomjs.org/download.html), unpack, and start having fun in just 5 minutes.

## Questions?

- Explore the complete [documentation](http://phantomjs.org/documentation/).
- Read tons of [user articles](http://phantomjs.org/buzz.html) on using PhantomJS.
- Join the [mailing-list](http://groups.google.com/group/phantomjs) and discuss with other PhantomJS fans.
- Join discussions at our [forum](http://discuss.phantomjs.org)

PhantomJS is free software/open source, and is distributed under the [BSD license](http://opensource.org/licenses/BSD-3-Clause). It contains third-party code, see the included `third-party.txt` file for the license information on third-party code.

PhantomJS is created and maintained by [Ariya Hidayat](http://ariya.ofilabs.com/about) (Twitter: [@ariyahidayat](http://twitter.com/ariyahidayat)), with the help of [many contributors](https://github.com/ariya/phantomjs/contributors). Follow the official Twitter stream [@PhantomJS](http://twitter.com/PhantomJS) to get the frequent development updates.
