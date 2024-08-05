# Douglas Little, Simons Foundation Coding Challenge Answers

## Question 1: Code Improvement.

For this question, I followed w3's example of a disclosure pattern. This pattern has "two elements: a disclosure button and a section of content whose visibility is controlled by the button."

To improve upon this code, we could add a visual indicator like a triangle to hint that the button will reveal hidden content.

For now, I've updated the button text to be more descriptive.

### Accessibility:

- The button to toggle the search form appearance has aria-controls and aria-expanded attributes. When the form is shown, the aria-expanded attribute will be true. The aria-controls attribute tells assistive devices which element the button controls.
- Each input has a required attribute. This allows for native browser validation when the form is submitted. The inputs will not be considered valid when they are submitted without content, and an error message will display.
- Since the anchor tag links back to the homepage, I"m assuming that this image is decorative, like a home-icon. I'm considering the image as decorative because I've added link text to the anchor tag, explaining that it links back to the homepage. The image would be considered supplementary to link text, or illustrative of adjacent text without contributing information. Because the image is decorative, adding an empty alt text will cause assistive technologies to ignore the image. This is desired because adding the alt text could add audible clutter to screen reader output.
- The img is now a png instead of a gif. Moving images should not auto-play, and they should have an interface to pause movement.
- Sort order input is now a `<select>` tag.

I left notes in the comments about what I would address next if I had more time.

### Legibility:

- HTML attributes all use double-quotes. Strings in JS use single-quotes. This is not a hard-fast rule, but Prettier in my IDE is configured this way.
- Comments are added in JS for each function and eventListener.
- Indentation is used and HTML attributes wrap after a certain amount.

### MISC (Scalability, Security, Performance):

- Generic classnames are removed.
- No longer checking the DOM for the existence of form elements, since we've wrapped our logic in an onload event.
- Removed the while loop from the submit function. Instead the searchMessage will display based on result of try/catch.
- Changed method to 'POST'.

## Question 2: Styling and Semantics

I went with a flex-box layout for the cards.

As a consideration for accessibility, I wrapped the cards in an unordered list. This provides more structural landmarks for the document. I also updated some of the generic markup to use semantic tags where applicable, for instance the `<header>` and `<main>` tags.

I found myself spending too much time on trying to nail the styling exactly on this one, and I had to move on to ensure I finished. The main thing that I couldn't crack is the maintaining of the size of the cards when the viewport shrinks. I added `flex-grow: 1` to my card items so that when the viewport shrinks for mobile, the cards will grow to take up the full-width of the viewport. With this value for flex-grow though, when the card items wrap on desktop and tablet, they're growing to take up the full-width. Without a media query and in the time alloted, I couldn't figure out how to exactly match the spec.

- **_THE FOLLOWING UPDATE WAS WRITTEN AFTER SUBMISSION WINDOW_**
  - In <a href="./update/StylingAndSemantics-update.html">this update file</a>, which was **created after the submission window**, I spent a few more minutes to get closer to the specification. In my original submission, I used flexbox for the card layout, but in the update I use CSS grid with auto-fill columns. Additionally, I extracted the svg from the external image so that it can be colored white.

## Question 3: Loading and Execution of JS

The problem with the initial definition of loadScript is that helloWorld will not be defined by the time it is called. This will result in a reference error.

To resolve this, we can try a few things. Like the example solution shows, we can use an onload event listener, which fires when a script has loaded. We can safely pass helloWorld as a callback in the onload event listener, and we'll know it's defined by the time it calls.

Another option that builds upon the example solution is to add `type="module"` to the script tag, which will allow us to use top-level `awaits`. If we then have loadScript return a promise, we can await the result before calling helloWorld. When the script's onload is fired, the promise will resolve.
