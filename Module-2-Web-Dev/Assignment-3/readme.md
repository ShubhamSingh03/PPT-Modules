# Assignment-3 Questions & Solutions

💡 **Question-1:**  What is a Media Query in CSS, and what is its purpose?

💬 **Solution-1:** 

A media query in CSS is a feature that allows to apply different styles or rules to a web page based on certain device characteristics, such as the screen size, device orientation, or the capabilities of the device. It enables responsive web design by adapting the layout and appearance of a web page to different screen sizes and devices.

The purpose of media queries is to create CSS rules that target specific devices or device characteristics and apply styles accordingly. By using media queries, we can customize the presentation of website to provide an optimal viewing experience across various devices, including desktops, laptops, tablets, and mobile phones.

Media queries are written using the `@media` rule in CSS.

Example:

```css
@media screen and (max-width: 600px) {
  /* CSS rules for screens with a maximum width of 600px */
  /* e.g., smartphones in portrait mode */
  body {
    background-color: lightblue;
  }
}
```

The above media query targets screens with a maximum width of 600 pixels (e.g., smartphones in portrait mode). In this case, the background color of the `body` element will be set to light blue for screens with a maximum width of 600 pixels.

By using media queries effectively, we can create responsive and adaptive designs that adjust and optimize the layout, typography, and other styles based on the user's device, providing a consistent and user-friendly experience across different screen sizes and devices.

<hr/>

💡 **Question-2:**  How do you define a media query in CSS?

💬 **Solution-2:** 

To define a media query in CSS, we use the `@media` rule followed by the desired condition or conditions. Here's the basic syntax for writing a media query:

```css
@media mediaType and (condition) {
  /* CSS rules to be applied when the condition is met */
}
```

- `@media`: This is the keyword that indicates the start of a media query.
- `mediaType`: It specifies the type of media to which the media query applies. The most common media types are `all`, `screen`, `print`, `speech`, etc. `all` is the default if no media type is specified. The `screen` media type is typically used for targeting devices with screens, such as computers, tablets, and mobile devices.
- `condition`: It represents the condition or set of conditions that determine when the CSS rules inside the media query should be applied. Conditions can include various features like screen width, height, aspect ratio, device orientation, resolution, and more. Multiple conditions can be combined using logical operators like `and` and `or`.

In the example below, the media query targets screens with a `screen` media type and a maximum width of `600px`. The CSS rules inside the media query block will be applied when this condition is met.

```css
@media screen and (max-width: 600px) {
  /* CSS rules for screens with a maximum width of 600px */
}
```

<hr/>

💡 **Question-3:**  Explain the concept of Breakpoints in Responsive Web Design and How They are used in Media Queries.

💬 **Solution-3:** 

In responsive web design, breakpoints are specific screen widths at which the layout and design of a website are adjusted to provide an optimal viewing experience. Breakpoints define the points at which the content and design of a web page need to adapt to different screen sizes and device capabilities.

Media queries play a crucial role in implementing responsive web design, and breakpoints are used within media queries to target specific ranges of screen widths. By using breakpoints in media queries, we can apply different CSS styles and layout adjustments to accommodate different devices and screen sizes.

Here's how breakpoints and media queries work together:

1. Determine Breakpoints:
   - The first step in implementing responsive web design is to determine the breakpoints at which our website's layout needs to change.
   - Breakpoints are typically chosen based on common screen sizes or device categories, such as mobile phones, tablets, and desktops.
   - Commonly used breakpoints are often associated with specific screen widths, such as 320px, 480px, 768px, 1024px, and 1200px.

2. Define Media Queries:
   - Once we have determined the breakpoints, we can create media queries in CSS to target specific screen widths and apply appropriate styles.
   - Media queries allow to specify different CSS rules based on the screen width or other conditions using the `@media` rule.
   - Each media query typically includes a condition that checks if the screen width is within a specific range or matches a particular device characteristic.
   - The CSS rules inside the media query block will be applied only when the condition is met.

3. Apply Responsive Styles:
   - Within each media query, we can write CSS rules that adapt the layout, positioning, typography, and other styles to optimize the presentation for the targeted screen size or device.
   - By applying responsive styles at different breakpoints, we can ensure that our website displays correctly and provides an optimal user experience on a variety of devices.

Example:

```css
/* Mobile styles */
@media screen and (max-width: 480px) {
  /* CSS rules for screens up to 480px */
}

/* Tablet styles */
@media screen and (min-width: 481px) and (max-width: 768px) {
  /* CSS rules for screens between 481px and 768px */
}

/* Desktop styles */
@media screen and (min-width: 769px) {
  /* CSS rules for screens above 769px */
}
```

These three media queries are defined with breakpoints at 480px, 768px, and 769px. Each media query targets a specific range of screen widths and applies different CSS rules accordingly.

<hr/>

💡 **Question-4:**  What is the purpose of using Media Queries for Print Media?

💬 **Solution-4:** 

The purpose of using media queries for print media is to apply specific styles and formatting when a web page is printed or viewed in print preview mode. Media queries for print allows to optimize the appearance of content when it is intended to be printed on paper or saved as a PDF.

Here are some reasons and use cases for using media queries for print media:

1. Print-specific Layout and Styling:
   - When a web page is printed, it often requires a different layout and styling compared to its on-screen presentation.
   - Media queries for print allows to define specific CSS rules that are only applied when the content is printed.

2. Hide Unnecessary Elements:
   - Certain elements, such as navigation menus, ads, or interactive features, may not be relevant or useful in a printed document.
   - Media queries for print enables to selectively hide or display elements based on their relevance to the printed output.

3. Adjust Typography and Page Formatting:
   - Printed materials often require specific typography adjustments, such as larger font sizes, different font families, or increased line spacing for readability.
   - Media queries for print allow us to modify typography-related CSS properties to optimize the text appearance on paper.

4. Custom Page Headers and Footers:
   - Media queries for print enables to define custom headers and footers that appear on every printed page.
   - This allows to include useful information such as page numbers, document title, date, or copyright information in the printed output.

Example:

```css
@media print {
  /* Print-specific styles */
  body {
    font-size: 14pt;
    line-height: 1.5;
  }

  nav, .advertisements {
    display: none;
  }

  h1 {
    page-break-after: avoid;
  }

  @page {
    margin: 2cm;
  }
}
```

Above media query targeting `print` is used to define print-specific styles. The `body` font size and line height are adjusted for better readability in print. The `nav` element and elements with the class `.advertisements` are hidden in the printed output. The `h1` headings avoid page breaks to prevent splitting across pages. The `@page` rule sets a 2cm margin for the printed pages.

<hr/>

💡 **Question-5:** What is the purpose of the orientation media feature?

💬 **Solution-5:** 

The purpose of the orientation media feature in CSS is to target and apply specific styles based on the orientation of the device's viewport. The orientation media feature allows to detect whether the device is in a portrait or landscape orientation and apply different CSS rules accordingly.

The orientation media feature is particularly useful for adjusting the layout and styling of a web page based on the device's orientation. By utilizing this feature one can optimize the presentation of content and ensure a better user experience on different devices.

The orientation media feature can have two possible values:

1. `portrait`: This value indicates that the device's viewport is taller than it is wide. It is commonly associated with vertical orientation.

2. `landscape`: This value indicates that the device's viewport is wider than it is tall. It is commonly associated with horizontal orientation.

Example:

```css
@media (orientation: landscape) {
  /* CSS rules for landscape orientation */
  /* e.g., adjust layout, positioning, or font sizes for horizontal view */
  body {
    background-color: lightblue;
  }
}
```

Defined media query targets devices with a `landscape` orientation and applies specific CSS rules inside the media query block. In this case, the background color of the `body` element is set to light blue when the device is in a landscape orientation.

<hr/>

💡 **Question-6:**

💬 **Solution-6:** 

```css

```

<hr/>

💡 **Question-7:**  You are tasked with building a webpage that displays an image gallery using a grid layout. The challenge is to ensure the gallery is visually appealing and functional on both large and small screens. On large screens, the gallery should display multiple images per row, while on small screens, it should collapse into a single column for optimal viewing. Refer to the attached images for visual reference. Implement this using CSS Grid and media queries for responsiveness.

💬 **Solution-7:** 

```css

```

<hr/>

💡 **Question-8:**

💬 **Solution-8:** 

```css

```

<hr/>

💡 **Question-9:**

💬 **Solution-9:** 

```css

```

<hr/>

💡 **Question-10:**

💬 **Solution-10:** 

```css

```

<hr/>