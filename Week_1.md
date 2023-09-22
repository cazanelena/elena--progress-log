## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/server/learning-outcomes/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.
> **[Learning outcome...]**
## Deploying our to a live on the fly.io server
- When we set up the package.json initally looked like this:
  ```JS
  "scripts": {
        "start": "nodemon src/index",
        "format": "npx prettier --write .",
        "test": "node --test",
    },
  ```
  - This meant that we would start our server locally using the command line "npm start". The "start" script in this configuration uses nodemon to automatically monitor and restart a Node.js application located in the "src/index" file whenever changes are detected.
  - But when we tried to deploy the app on the fly.io the Dockerfile would try to start the machine using the same command rather the "node src/index".
  - This would not allow our app to be successfully deploy and the status on the fly.io dashboard will appear as "Suspended"
  ## How we fixed the problem?
  We updated the package.json and added a new command "start2": "node src/index" and change the dockerfile accordingly.
   
> [your evidence here]
<img width="750" alt="Screenshot 2023-09-19 at 14 51 02" src="https://github.com/fac28/elena--progress-log/assets/59057287/5e50c240-e648-4d1a-a24d-fb9664cf929f">
<img width="634" alt="Screenshot 2023-09-19 at 14 51 40" src="https://github.com/fac28/elena--progress-log/assets/59057287/6bca3bc1-6f28-4100-a997-b447b238d92b">



 ### 2. Show an example of a learning outcome you have struggled with and/or would like to re-visit.
 
 
> [**Learning outcome...**]
## Set up continuous deployment to a live production server
For this I followed this tutorial: https://fly.io/docs/app-guides/continuous-deployment-with-github-actions/
Once everything was setup and we would push a change into the main then the deployment should be automatically triggered. Unfortunately, this didn't happen the deployement got stack in an infinite loop, not GitHub actions would be triggered either. 
I tried to follow a different approach and set up the workflow from the GUI interface: 

![Screenshot 2023-09-22 at 10 19 57](https://github.com/fac28/elena--progress-log/assets/59057287/cd329eb9-55e3-4e96-ae86-4b113d31e2bd)

This solved the issue and each time there was a new change to the main branch the deployment happened automatically.

```JS
name: Fly Deploy
on:
  push:
    branches:
      - main
jobs:
  deploy:
    name: Deploy app
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: superfly/flyctl-actions/setup-flyctl@master
      - run: flyctl deploy --remote-only
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
```

## Feedback
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
