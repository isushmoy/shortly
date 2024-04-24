# Shortly

This app empowers users to effortlessly shorten URLs with its user-friendly interface. It leverages the CleanURI API, Clipboard API, and advanced CSS for seamless functionality. Additionally, CORS proxy is utilized for enhanced API integration.

Live Site: [Shortly](https://sushcod3.github.io/shortly/)

## Table of contents

- [Features](#features)
- [Screenshot](#screenshot)
- [Technologies Used](#technologies-used)
- [Lessons Learned](#lessons-learned)
- [Acknowledgments](#acknowledgments)

### Features

- Easily shorten any valid URL.
- Access a list of your shortened links, which persists even after refreshing the browser.
- Copy the shortened link to your clipboard with a single click.
- Click on shortened links to open them directly in a new page.
- Clear button to remove all shortened URLs from the list.
- Enjoy an optimal layout tailored to your device's screen size for a seamless user experience.

### Screenshot

![Desktop Screenshot](./public/screenshot-desktop.jpeg)

### Technologies Used

- [CleanURI API](https://cleanuri.com/docs)
- [Clipboard API](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/)
- Vuejs
- CSS
- Bootstrap

### Lessons Learned

1. Starting with a mobile-first approach proved to be more effective for me.
2. Employing `navigator.clipboard.writeText(index)` enables copying text to the clipboard using JavaScript.
3. Utilizing the `:not()` pseudo-class in CSS allows styling all elements except those specified inside the `:not()` selector.
4. To use `mx-auto` properly, apply it to a block-level element with a defined width.
5. When confused, adding an outer div container can help organize layout.
6. `JSON.parse()` converts strings into JavaScript objects, often used for API responses.
7. In Vue.js, `computed` properties reactively update based on changes, while `watch` is used for side effects.
8. Utilized [CORS proxy](https://corsproxy.io/) to bypass CORS restrictions when accessing the public endpoint of CleanURL API.

### Acknowledgments

This project is a solution to the challenges provided by [Frontend Mentor](https://www.frontendmentor.io/solutions/efficient-age-calculation-with-javascript-and-vuejs-validation-L9dCXc8B0f), with additional features implemented by me.
