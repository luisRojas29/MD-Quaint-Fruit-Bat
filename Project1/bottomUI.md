---
#BottomUI
---

An explanation of how the code works in the bottom half of the page.

- Spacing and layout
	- Id= "#BottomUI"
		- A wrapper for the full page bottom which sets the total bottom of the page to 100vw of the screen.  This means that the page which base its width on the full width of the screen accessing the page.  The vw unit stands for "view width" and you can find more information on that [here](https://web-design-weekly.com/2014/11/18/viewport-units-vw-vh-vmin-vmax/).  This allows us to, when appropriate, use a % unit for width calculations, and the browser will scale accordingly based on the user's device width.
	- id = "#panelsLocation"
		- Another wrapper but for our panels only.  This immediately takes advantage of our above viewpoint setting.  We want our panels to have a margin of about 7.5% on both sides.  But settings margins manually can get tricky when dealing with different device sizes.  This ID works by making the container for our panels 85% of the page width and then placing that div smack middle of the page horizontally.  Notable options are.
			- display: block
				- Needed for automatic centering option.  Will not work with other display modes.
			- margin: 0 auto;
				- Horizontally centers a block element
			- overflow: hidden
				- This is a bit out a hack.  We use floating elements in our page which do not get included in the divs height because they are technically outside the page flow.  Since we need to set a bottom margin of our page here we need the height: auto setting to work correctly.  The overflow: hidden fixes this issue.  More information [here](http://www.quirksmode.org/css/clearing.html).
			- width: 85%
				- Remember, we set our viewwidth to 100vw?  This setting is what creates our margin.
				- TRY THIS:  Set the width to 50%.  See what happens.  Now set it to 30%, 70%, etc.

- Panel Options (For both panels)
	- class = ".bothPanels"
		- Our panels need to be the same equal width and height.  This class is given to both our left and right panel so that shared settings can be modified here quickly, and we can immediately see how that affects the total page layout.
		- NOTE:  Never change the height, width, margins, or padding of the individual panels.  Any changes to those settings should be done here to make sure our panel boxes remain identical.
		- The width of our panels is calculated reactively and does not really ever need to be changed.  Our panels should always be centered in the page, equal width, with a ruler in between.  The setting is 47.5%.  But remember...
			- BottomUI is 100vw
			- panelLocation is 85%
		- ...So really this means 47.5% of 85% based on a viewwidth of 100vw.  
			- The remaining 5% gives us space for our ruler image- in the center.  So the only time you'd want to change the width is if you want more space for the ruler.
		- Noted options:
			- float:left
				- Makes the three separate areas (both panels and the ruler) "hug" giving the illusion of a single design. 
			- box-sizing: border-box
				- Left panel is a div, but right panel is a textarea.  These elements have different defaults for how they handle margins and padding and if you make a change in the ".bothPanels" class there will still be slight differences between them.  By setting this class to border-box these differences are accounted for when resizing.  Again, this allows for quick changes without having to manually adjust a bunch of margins if we want to adjust our layout sizes.
		- TRY THIS:  Change the height of ".bothPanels" from its current setting of 31.25rem to 30rem.  Now try 25rem.  See how the panels and the ruler adjust accordingly?  No additional adjustments are needed.


- The Ruler
	- In our HTML, our ruler has a class of ".bothPanels" and an ID of "#ruler."  In your last pull request you remove the ".bothPanels" class from the ruler.  I  understand why you did this because it's not immediately intuitive what's going on here.  Here's the deal: our ruler HAS to be the same height as our panels.  Giving it the same class as our panels accomplishes just that.  We then use our ID "#ruler" to change the width.
		- Remember this: when given two values for the same element, CSS will always use the value adjusted last.  This is why this works.  Technically, changing the width on ".bothPanels" changes the width of the ruler, but since we have a new width rule at "#ruler" that occurs AFTER that, the borwser "fixes" this issue for us.
	- TRY THIS:  Remove class ".bothPanels" from the ruler in HTML.  Now, go back to CSS and change the height in class ".bothPanels."  You'll see the ruler now longer adjust to our panels.

- The Left Panel
	- Is made up of three separate divs:
		- ".panelTabs"
		- ".panelBody"
		- ".panelChat"
	- The heights of three divs are currently:
		- ".panelTabs" 10%;
		- ".panelBody" 62%
		- ".panelChat" 28%
			- This allows our leftPanel proper scaling.
		- If you need to add more space for the elements in one of these divs, you have to change all div heights so that they always add up to 100%.   For example, if you want to make the tabs larger, you could make .panelTabs 12%, but then you need to adjust .panelBody to 60% to compensate.