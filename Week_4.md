## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/server-side-app/schedule/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.

> This week I learned how to setup Sentry and monitor the performance of our app. 

```js
const Sentry = require("@sentry/node");

const sentryDSN = process.env.SENTRY_DSN;
Sentry.init({
  dsn: sentryDSN,
  release: "ai-art-gallery@" + process.env.npm_package_version,
  integrations: [
    // enable HTTP calls tracing
    new Sentry.Integrations.Http({ tracing: true }),
    // enable Express.js middleware tracing
    new Sentry.Integrations.Express({
      // to trace all requests to the default router
      server,
      // alternatively, you can specify the routes you want to trace:
      // router: someRouter,
    }),
  ],

  tracesSampleRate: 1.0,
});

// The request handler must be the first middleware on the app
server.use(Sentry.Handlers.requestHandler());
// TracingHandler creates a trace for every incoming request
server.use(Sentry.Handlers.tracingHandler());

```
If there will be any issues or bugs Sentry will send us automatic alerts with here the problem was located.

<img width="825" alt="Screenshot 2023-10-12 at 15 59 42" src="https://github.com/fac28/elena--progress-log/assets/59057287/19664567-b15d-47af-a67b-b45ad733b8a3">

Used Fly.io to monitor the memory usage. This helped me tackle why our app was crashing during the code reviews. 

<img width="534" alt="Screenshot 2023-10-12 at 16 00 43" src="https://github.com/fac28/elena--progress-log/assets/59057287/033f3ce7-fed0-44fa-8643-1d000f754eca">


 ### 2. Show an example of a learning outcome you have struggled with and/or would like to re-visit.

> Saving file upload to the database (images). I haven't wrote the code, but would be nice to revisit this.

> When a user sends a POST request to the route, it checks if the uploaded file is an image (JPEG or PNG) and if it's under 5 megabytes in size. If these conditions are met, it stores the image as a base64-encoded string, inserts information about the image into a database, and redirects the user to a different page. If the conditions are not met, it returns an error response. The GET request to the same route returns a form for file upload.

```js
const multer = require("multer");
const upload = multer({ storage: multer.memoryStorage() });
const MAX_SIZE = 1000 * 1000 * 5; // 5 megabytes
const ALLOWED_TYPES = ["image/jpeg", "image/png"];

router.get("/", (req, res) => {
  return res.send(form());
});

router.post("/", upload.single("avatar"), (req, res) => {
  // req.file is the `avatar` file
  const fileImg = req.file;

  if (!ALLOWED_TYPES.includes(fileImg.mimetype)) {
    res.status(400).send("<h1>File upload error</h1><p>Please upload an image file</p>");
  }

  if (fileImg.size > MAX_SIZE) {
    res.status(400).send("<h1>File upload error</h1><p>Profile picture must be < 5MB</p>");
  } else {
    // req.body will hold the text fields, if there were any
    const { name, description } = req.body;
    let tags = req.body.action;

    if (!tags) {
      tags = [];
    }

    const tagsString = tags.join(", ");

    const imageBuffer = fileImg.buffer.toString("base64");
    const imageId = insertImage(imageBuffer).id;
    insertArtworkDetails(description, imageId, name, tagsString);

    res.redirect("/");
  }
});

```

## Feedback
### Alphonso's feedback
#### What Went Well
Great work with Sentry. The explanation you gave during presentations about tracking and addressing the issue with memory usage during the code reviews was particularly insightful.
Maybe you could even repurpose those slides for documentation like this progress log or your portfolio.
Also have a think about maybe visiting one of your suggested solutions in a larger project, like the upcomming in-house build. Could there be a case for applying queueing, for example? 

#### Even Better If
[Tommaso's progress log](https://github.com/fac28/Tommaso-progress-log/blob/main/Week_4.md) has a pretty detailed run down of the setup of Multer that might be useful for you if you want to give this a try in a future project.
