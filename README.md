# Trump-Qoute-Generator
Genereates trump qoutes
Dont care what you do

HTML Code:
<html>
<div class="app">
  <header>Random Donald Trump Quotes</header>
  <section class="quotes">
    <div class="quote-text" id="js-quote-text"></div>
  </section>
  <div id="js-spinner" class="spinner hidden">
    <div class="rect1"></div>
    <div class="rect2"></div>
    <div class="rect3"></div>
    <div class="rect4"></div>
    <div class="rect5"></div>
  </div>
  <section class="controls">
    <button type="button" id="js-new-quote" class="new-quote button">
      Generate a new quote
    </button>
    <a class="twitter button" id="js-tweet" target="_blank" rel="noreferrer">Tweet it!</a>
  </section>
</div>
</html>

Java Script(No Libraries):
const twitterButton = document.querySelector('#js-tweet');
const spinner = document.querySelector('#js-spinner');
const newQuoteButton = document.querySelector('#js-new-quote');
newQuoteButton.addEventListener('click', getQuote);

const endpoint = 'https://api.whatdoestrumpthink.com/api/v1/quotes/random';

async function getQuote() {
  spinner.classList.remove('hidden');
  newQuoteButton.disabled = true;

  try {
    const response = await fetch(endpoint)
    if (!response.ok) {
      throw Error(response.statusText);
    }
    const json = await response.json();
    displayQuote(json.message);
    setTweetButton(json.message);
  } catch {
    alert('Failed to fetch new quote');
  } finally {
    newQuoteButton.disabled = false;
    spinner.classList.add('hidden');
  }
}

function displayQuote(quote) {
  const quoteText = document.querySelector('#js-quote-text');
  quoteText.textContent = quote;
}

function setTweetButton(quote) {
  twitterButton.setAttribute('href', `https://twitter.com/share?text=${quote} - Donald Trump`);
}

getQuote();

CSS:
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
  background-color: #c9bd95;
}

.app {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 600px;
  background-color: white;
  border-radius: 5px;
  box-shadow: 0 2px 2px 0 rgba(0,0,0,.14), 0 3px 1px -2px rgba(0,0,0,.2), 0 1px 5px 0 rgba(0,0,0,.12);
}

header {
  width: 100%;
  font-size: 30px;
  text-align: center;
  padding: 10px;
  border-bottom: 1px solid #ebebeb;
}

.quotes {
  padding: 20px 50px;
  min-height: 200px;
}

.quote-text {
  padding-bottom: 20px;
  font-size: 25px;
  color: black;
}

.controls {
  width: 100%;
  padding: 20px 50px;
}

.button {
  display: block;
  color: white;
  border-radius: 4px;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  text-align: center;
  width: 100%;
  font-size: 20px;
  box-shadow: 0 2px 2px 0 rgba(0,0,0,.14), 0 3px 1px -2px rgba(0,0,0,.2), 0 1px 5px 0 rgba(0,0,0,.12);
}

.twitter {
  background-color: #1da1f2;
  text-decoration: none;
}

.twitter:hover {
  background-color: #1e7fbb;
}

.new-quote {
  background-color: #4A2B0F;
  margin-bottom: 15px;
}

.new-quote:hover {
  background-color: #6d3b0e;
}

.new-quote:disabled {
  background-color: #cccccc;
  color: #666666;
  cursor: not-allowed;
}

@media screen and (max-width: 60px) {
  .app {
    width: 100%;
  }
  .quote-text {
    font-size: 8px;
  }
}

.spinner {
  margin: 10px auto;
  width: 50px;
  height: 40px;
  text-align: center;
  font-size: 10px;
}

.spinner.hidden {
  visibility: hidden;
}

.spinner > div {
  background-color: #333;
  height: 100%;
  width: 6px;
  display: inline-block;

  -webkit-animation: sk-stretchdelay 1.2s infinite ease-in-out;
  animation: sk-stretchdelay 1.2s infinite ease-in-out;
}

.spinner .rect2 {
  -webkit-animation-delay: -1.1s;
  animation-delay: -1.1s;
}

.spinner .rect3 {
  -webkit-animation-delay: -1.0s;
  animation-delay: -1.0s;
}

.spinner .rect4 {
  -webkit-animation-delay: -0.9s;
  animation-delay: -0.9s;
}

.spinner .rect5 {
  -webkit-animation-delay: -0.8s;
  animation-delay: -0.8s;
}

@-webkit-keyframes sk-stretchdelay {
  0%, 40%, 100% { -webkit-transform: scaleY(0.2) }
  20% { -webkit-transform: scaleY(0.5) }
}

@keyframes sk-stretchdelay {
  0%, 40%, 100% {
    transform: scaleY(0.2);
    -webkit-transform: scaleY(0.2);
  }  20% {
    transform: scaleY(0.5);
    -webkit-transform: scaleY(0.5);
  }
}

