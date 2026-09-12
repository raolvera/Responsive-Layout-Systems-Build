# Layout Notes and Testing Evidence
Project: ASU Sun Devils Football Gameday Hub
Author: Rey Olvera
Course: GIT 515 Advanced Web Coding
Professor: Hillerman 
Module: 3 – Responsive Layout System
Date: September 13, 2026


## Overview

This build adds to the Module 2 stylesheet. It does not replace it. The colors, the file order, and the mobile first setup all stayed the same. I only added new things on top. Below is what I changed from the old Module 2 CSS.The full responsive stylesheet with the remaining capstone pages and real images to follow their nav links and image spots are held with TODO comments.

## 1. Responsive layout foundation

The goal here was to make the page wrappers, sections, and spacing flexible instead of locked to fixed sizes. The old container, main and section rules used fixed widths and plain left, right, and top spacing. I switched them to logical spacing so the layout follows the reading direction, and I made the spacing flex with the space it has instead of being one set number. I tested it by shrinking the window down to a small phone size and checking that the page still fit with no sideways scroll bar (MDN logical).

## 2. Advanced Grid patterns

Here I built two grid layouts that size themselves from the content. The old card grid changed its number of columns by hand at 768 and 1000 pixels, and it was the only grid on the site. I rebuilt it so it works out its own number of columns based on the space it has. I also added a second grid, the Gameday at a Glance stat grid, that does the same thing. I tested both by dragging the window slowly from narrow to wide and watching the columns add and drop on their own with no sudden jump (MDN minmax).

## 3. Subgrid or documented alternative

I used subgrid where it helps things line up. The old CSS did not use subgrid because nothing needed to line up across cards. The new stat cards do, so I used subgrid to keep each card's label and value on the same line across the whole row, no matter how long the text is. I tested it by giving one card a longer label and checking that the values in the other cards still lined up (MDN subgrid).

## 4. Container-query component

In the old CSS everything reacted to the screen size only, so nothing reacted to its own space. I built a spotlight block that reacts to the width of its own box. It stacks when its box is narrow and sits side by side when its box is wide, so the same block works in any spot on the page. I tested it by resizing the area it sits in and watching it change layout on its own (MDN container).

## 5. Content driven breakpoints

I switched to breakpoints based on actual layout behavior. The old CSS included tablet at 768px and desktop at 1000px, but the new grid adjusts on its own, so those weren’t necessary anymore.

The only breakpoint I kept is the one that affects the navigation bar. I widened the browser window until the logo and nav links stopped fitting on the same row. That happened around 992px, so that breakpoint is now tied to the layout’s real needs rather than a device category. This follows MDN’s guidance on responsive, content‑first breakpoints.

## 6. User preferences

I added at least one setting that respects what the user prefers, like less motion, more contrast, or a color scheme. The old CSS only handled less motion. I added a higher contrast option next to it that makes the borders and the focus outline stronger, and it only changes a few values so the brand colors stay the same. I tested it by turning on the higher contrast setting in the browser tools and checking that the borders and focus outline got stronger while the colors stayed the same (MDN media).

## 7. Feature and fallback strategy

I checked that if feature was supported and provide a backup path if it is not. The old CSS had one check for Grid with a flexbox backup. I added a check around each of the two new features, so subgrid and the container feature each have one. If a browser does not support them, it uses a simpler layout that still works instead of breaking. I tested the backup by turning the container feature off in the browser tools and checking that the spotlight just stayed stacked and readable (MDN supports).

In plain terms, if Grid is not supported the cards stay a simple wrapped row. If subgrid is not supported the stat cards keep their normal rows and stay readable. If the container feature is not supported the spotlight just stays stacked. Every backup keeps the content usable.

## 8. Testing evidence

I checked the page at narrow, medium, and wide sizes, at 200 percent zoom, and with the keyboard only. I did this in Chrome and Firefox on Windows, using the browser Responsive Design Mode and by resizing the window.

At a narrow size, around 360 to 640 pixels, the layout dropped to a single column. The card grid showed one full-width column and the stat grid kept two columns to use the space, and the nav links were hidden, which shows it switched to the menu state. At a medium size, around 700 pixels, the stat grid opened up while the card grid moved from its stacked phone layout toward a multi-column desktop grid. At a wide size, 1280 pixels, the Quick Links section filled three columns, the spotlight sat side by side, and the nav took up a full row.

For zoom I set the page to 200 percent at a 1280 pixel width to check the reflow rule from the accessibility guidelines. The content stacked into one readable column with no sideways scroll and no overlapping text. For the keyboard I tabbed through the page. The skip link is placed with absolute positioning and shows up on the first tab, every link and button has a clear focus outline, and the tab order follows the page structure, going header, hero, main, then footer.

I also checked the user settings and the backups. For less motion I turned on the reduced motion setting, and the CSS transitions stopped. For higher contrast I turned that setting on and confirmed the borders and focus outlines stayed easy to see against the background. For the backup I turned off container query support, and the spotlight and card pieces fell back to their normal grid layouts and stayed usable and readable.

A couple of notes. Every image on the site, including images/stadium.png and the other picture spots, is just a placeholder for now. I am using them to hold the layout in place and will put the real pictures in later. Because of that they may show as a broken-image box, but the layout around them stays fine, since the grid boxes are sized to hold the content whether or not the image loads. This check shows the site is ready for a final screen reader pass and a full accessibility review.

One more note on validation. When I run the CSS through the W3C validator it reports a few errors on the spotlight block, saying container-type and container-name do not exist and that @container is an unrecognized at-rule. These are false negatives, not real problems. Container queries are standardized CSS and have been supported in every major browser since 2023, but the W3C validator's rule set predates that support and does not recognize them yet. The same reason explains the "CSS variables are currently not statically checked" warnings, the validator does not evaluate var() custom properties, and the vendor-extension warnings for -webkit-text-size-adjust, -webkit-overflow-scrolling, and ::-webkit-details-marker, which are intentional prefixes I added for iOS and Safari. I left all of these in place on purpose. The container-query code is wrapped in an @supports (container-type: inline-size) feature query with a documented stacked fallback, so browsers that do not support it still get a usable layout, and browser DevTools show no console errors on the page.

## 9. AI disclosure

I used AI within the allowed scope, which is that AI may explain syntax, suggest edge cases, or help troubleshoot. It explained how the newer CSS features work and pointed out edge cases. I wrote and set up the CSS myself and checked all of it in the browser using the tests in part 8, so the results come from my own testing.

## References

MDN Web Docs. CSS logical properties and values. Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_logical_properties_and_values

MDN Web Docs. minmax(). Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/minmax

MDN Web Docs. repeat(). Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/repeat

MDN Web Docs. Subgrid. Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Subgrid

MDN Web Docs. Container queries. Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_queries

MDN Web Docs. Using media queries. Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries

MDN Web Docs. @supports. Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/@supports

MDN Web Docs. clamp(). Mozilla. https://developer.mozilla.org/en-US/docs/Web/CSS/clamp

MDN Web Docs. Responsive design. Mozilla. https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design

W3C. Understanding Success Criterion 1.4.10 Reflow. World Wide Web Consortium. https://www.w3.org/WAI/WCAG21/Understanding/reflow.html
