# Usability & Accessibility

At its most basic, __usability__ is about making something straightforward for the average user to understand and access. __Accessibility__ is about supporting users who have additional barriers, such as a disability, a slow connection or an old computer.

## Usability


### What is usability?
Web usability is the ease of use of a website:
 - The presentation of information and choices in a clear and concise way.
 - Lack of ambiguity and the placement of important items in appropriate areas.
 - Ensuring that the content works on various devices and browsers.
 - Ensuring that the website is appropriate for all ages and genders.

### Key principles to achieve usability:
  1. Availability and Accessibility - if someone tries to access your site and it doesn't work for some reason, then your website becomes worthless.
  2. Clarity - users visit your site for a specific goal, do not confuse the user and help them reach their goal as quick as possible.
  3. Learnability - aim for an intuitive interface, an interface that doesn't require instructions. the key to intuitive design is to either use what people already know or create something that is easy to learn.
  4. Credibility - if the user doesn't trust you, the content on the website is worthless.
  make sure the site has an About us page including contact details.
  5. Relevancy - It is not enough that your website is clear, your content must also be relevant.

### Examples

One of the best known and frankly most surprising examples of user-centred design in the UK is the government's one-stop digital shop, [GOV.UK](https://www.gov.uk/).

The overhaul of the government's web properties was based on [a series of recommendations](https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/60993/Martha_20Lane_20Fox_s_20letter_20to_20Francis_20Maude_2014th_20Oct_202010.pdf) made by Martha Lane Fox in 2010. At the core of the recommendations she made was 'revolution not evolution' - she recomended that users must be the focus of the redesign of online government services.

Government Digital Service (GDS) was founded in 2011
as part of the Cabinet Office to undertake the digital transformation of government.

In 2013 GOV.UK won the Design Museum's prestigious 'Designs of the Year' award for its user-centred design. GDS is quoted in the [Guardian](https://www.theguardian.com/artanddesign/2013/apr/16/government-website-design-of-year), saying: "We've removed everything that gets in the way of fast and easy access to information."

#### To get an understanding of the process and principles behind GOV.UK take a look at the following resources:
1. [Recommendations from Martha Lane Fox](https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/60993/Martha_20Lane_20Fox_s_20letter_20to_20Francis_20Maude_2014th_20Oct_202010.pdf)
2. [Video of Tom Loosemore talking about how to build user-centred software products](https://vimeo.com/58798945) (strongly recommended)
3. [GOV.UK design principles](https://www.gov.uk/design-principles)

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
```
<label for="name">Name:</label>
<input id="name" type="text" name="textfield">
```
- Semantic HTML tags and IDs
- Role attribute in HTML (gives information to screen readers, e.g. tablist)
```
<li class='navbar__liitem'>About</li>
<li class='navbar__liitem' role="menu">Authors
  <ul class='dropdown'>
    <li class='subnavbar__liitem' role="menuitem">Cleo</li>
    <li class='subnavbar__liitem' role="menuitem">Jen</li>
    <li class='subnavbar__liitem' role="menuitem">John</li>
    <li class='subnavbar__liitem' role="menuitem">Esraa</li>
  </ul>
</li>
```

```
<form role=search>
```
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
