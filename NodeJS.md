#Development 
It is a runtime environment that allows us to execute [[JavaScript]] outside of a web browser.
### Architecture
All browsers have a JavaScript engine to read and render (graphically represent) JavaScript code. This makes the language dependent on a browser to be executed. Browsers use different engines, and it is because of this variety that sometimes the same JavaScript code can behave differently depending on the browser in which it is executed.
- Internet Explorer: Chakra Engine
- Mozilla Firefox: SpiderMonkey Engine
- Google Chrome: V8 Engine
NodeJS is built on the V8 engine of Google Chrome. This makes it a JavaScript runtime environment and allows the language to be executed without depending on a browser. In this way, we can program both the front-end and the [[Back-end Development|back-end]] in the same language: JavaScript.