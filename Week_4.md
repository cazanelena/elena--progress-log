## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/server-side-app/schedule/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.
> **[Learning outcome...]**  
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
> [**Learning outcome...**]  
> [your evidence here]

## Feedback
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
