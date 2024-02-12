# CSS
**1. What is CSS?**

- **Answer:** CSS stands for Cascading Style Sheets. It is a style sheet language used to describe the presentation of a document written in HTML or XML, including the layout, colors, fonts, and spacing.

**2. Explain the concept of "Cascading" in CSS.**

- **Answer:** Cascading refers to the order of priority that the browser follows when applying multiple style rules to an HTML element. It follows a specific hierarchy: inline styles (highest priority), internal or embedded styles, and external styles (lowest priority).

**3. What is the box model in CSS?**

- **Answer:** The CSS box model is a design principle that represents elements on a webpage as a rectangular box. It consists of content, padding, border, and margin.

**4. Describe the difference between `display: block`, `display: inline`, and `display: inline-block`.**

- **Answer:**
    - **`display: block`**: Makes the element a block-level element, forcing a line break before and after it.
    - **`display: inline`**: Makes the element an inline element, allowing it to flow within the text on the same line.
    - **`display: inline-block`**: Combines features of both block and inline elements. It allows the element to have block-level properties while flowing within the text like an inline element.

**5. What is the clearfix hack?**

- **Answer:** The clearfix hack is a technique used to fix issues related to the container not properly containing its floated children. It typically involves adding a clearfix class to the container or using the **`::after`** pseudo-element with clear properties.

**6. Explain the difference between `margin` and `padding`.**

- **Answer:**
    - **`Margin`**: It is the space outside the border of an element. It contributes to the total space an element occupies on the page, affecting the layout of neighboring elements.
    - **`Padding`**: It is the space between the content and the border of an element. It affects the content area's size but doesn't contribute to the overall size of the element on the page.

**7. What is the purpose of the z-index property?**

- **Answer:** The z-index property is used to control the stacking order of positioned elements along the z-axis. Elements with a higher z-index value will appear above elements with a lower z-index value.

**8. How can you center an element horizontally and vertically in CSS?**

- **Answer:**
    - Horizontally: Use **`margin: 0 auto;`** on a block-level element with a specified width.
    - Vertically: Use the combination of **`position: absolute;`**, **`top: 50%;`**, and **`transform: translateY(-50%);`** on a container element with a specified height.

**9. What are media queries in CSS?**

- **Answer:** Media queries are CSS techniques that allow the presentation of a document to be tailored to a specific range of output devices or screen sizes. They are commonly used in responsive web design to apply different styles for different devices or screen widths.

**10. What is the difference between `em` and `rem` units in CSS?**

- **Answer:**
    - **`em`**: It is a relative unit that is based on the font-size of the nearest parent element or the element itself.
    - **`rem`**: It is a relative unit that is based on the font-size of the root element (html).