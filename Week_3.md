## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/authentication/learning-outcomes/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.
CookieParser and using hidden variables. This was set up locally on the package.json but once the app was deployed to fly.io will automatically crash because the cookies secret was not visable to the fly server. To fix this I went on the fly's documentation and bewlow was the command line that fixed my problem. :) 
 <img width="815" alt="Screenshot 2023-10-05 at 10 58 48" src="https://github.com/fac28/elena--progress-log/assets/59057287/47556b95-69c9-491f-bc76-4450f1593c2f">


 ### 2. Show an example of a learning outcome you have struggled with and/or would like to re-visit.
We created a file called templates where ended up adding all our functions that will generate our html. After we created all the functions example below, realised that they didn't have a "head" or "body" tag. 

```JS
function signUpPage() {
return html*/ `
  <div class="signup-wrapper">
    <div class="signup-container">
        <h1 class="signup-heading">Register here</h1>
        <form method="POST" action="/sign-up" class="signup-form">
            <div class="form-group">
                <label for="email" class="form-label">Email</label>
                <input type="email" id="email" name="email" class="form-input" required>
            </div>
            <div class="form-group">
                <label for="password" class="form-label">Password</label>
                <input type="password" id="password" name="password" class="form-input" required>
            </div>
            <button type="submit" class="signup-button">Sign up</button>
        </form>
    </div>
</div>
`;
}
```

For that we decided to add another function called Layout() and this will insert the <>head</head> and <>body</body> tags. This will take 3 args: title, content and style (the path used to connect the html with the right css file).

```JS
function layout(title, content, style) {
  return /*html*/ `
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>${title}</title>
      <link rel="stylesheet" href="${style}">
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Inter:wght@200;300;500;900&display=swap" rel="stylesheet">
  </head>
    <body>
      ${content}
    </body>
  </html>
  `;
}
```
Our functions end up like the 👇 

```
function homePage() {
  const title = "Home page";
  const style = "style.css";
  const content = /*html*/ `
  
  <div class="hero">
    <div class="container">
      <div class="container1">
        <h1 class="title">Bookmarks</h1>
        <h2 class="sub-title">The top secret bookshelf, shhhh</h2>
      </div>
      <div class="container2">
        <a href="/sign-up" class="button">Sign up</a>
        <a href="/log-in" class="button">Log in</a>
      </div>
    </div>
  </div>
  `;
  return layout(title, content, style);
}
```

Ideally, in the future I would split the templates file in different files because it become a bit difficult to read and navigate.

## Feedback
> Beth

> Your understanding of the deployment logs is excellent 👏

> When splitting files, it’s a good idea to ensure that each file/module does just one thing. This will be less of an issue when you switch to react next week.
A useful resource on environment variables in node.js: [working-with-environment-variables-in-node-js-html](https://www.twilio.com/blog/working-with-environment-variables-in-node-js-html)
