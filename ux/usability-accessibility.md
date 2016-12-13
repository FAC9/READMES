# usability and accessibility

Intro


## usability

What is usability?

List of resources


## accessibility

### What is accessibility?

The World Wide Web Consortium defines web accessibility as an attribute through which “people with disabilities can perceive, understand, navigate, and interact with the web, and they can contribute to the web”.

Web accessibility includes all types of disabilities that impact access to the web and thus includes visual, auditory, physical, speech, cognitive and neurological disabilities and adherence to web accessibility principles also benefits elderly users.

So as to improve web site accessibility, the World Wide Web Consortium (W3C) has set up the Web Accessibility Initiative (WAI) which publishes the Web Content Accessibility Guidelines (WCAG) – a set of guidelines with the aim of making the web content more accessible to people with disabilities and indirectly to users in general.


This might include:

- Users of screen readers (blind or partially-sighted users)
- Color blind users
- Users with hearing impairments
- Users with low dexterity
- Users with terrible computers (!)


### A few simple steps towards accessibility

- Alt text on images
- Color contrast (accessibility for users with colour blindness)
- Indicate language of the page in HTML page head (or around sections of text on your page that are in another language, or around abbreviations) for screen readers (```lang="en_gb"```)
- Resizeable text
- Labels on forms (useful guidelines [here](http://www.bbc.co.uk/guidelines/futuremedia/accessibility/html/form-labels.shtml  ))
- Semantic HTML tags and IDs
- Role attribute in HTML (gives information to screen readers, e.g. tablist)
- Transcripts for audio files
- All functionality available via keyboard, e.g. tabbing or using arrow keys to navigate around (some users can't use a mouse - use tabindex!)
- Consider users with dyslexia when deciding on line-height / text alignment / font


### List of useful terms

[Aria-label attribute](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute)

[Tab index](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)


### Test your web apps!

http://khan.github.io/tota11y/

Totally is a great Chrome extension that will visualise how your site performs with assistive technologies.


### More resources

Official line on accessibility: https://www.w3.org/WAI/intro/wcag

BBC's guidelines on accessibility: http://www.bbc.co.uk/accessibility/best_practice/standards.shtml

More from the BBC: http://www.bbc.co.uk/accessibility/best_practice/what_is.shtml

Businesses who don't make their websites accessible could be sued for discrimination under UK law: http://www.out-law.com/page-330

More about discrimination from the Guardian: https://www.theguardian.com/sustainable-business/2015/dec/31/digital-discrimination-netflix-disney-target-web-accessibility-doj

Udacity have a free course! https://www.udacity.com/course/web-accessibility--ud891

Good article about usability and accessibility: http://blog.careerfoundry.com/ux-design/the-importance-of-usability-and-accessibility-in-design
