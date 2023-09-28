## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/database/learning-outcomes/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.
 - GitHub Actions CI setup to run your tests when you push
   <img width="659" alt="Screenshot 2023-09-28 at 16 00 00" src="https://github.com/fac28/elena--progress-log/assets/59057287/f4ab229c-27e5-455c-b1b5-57475a30936f">


> **[Learning outcome...]**  
> [your evidence here]

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
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18.16.0' 

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
        
      - name: Set up Flyctl
        uses: superfly/flyctl-actions/setup-flyctl@master
        with:
          api-token: ${{ secrets.FLY_API_TOKEN }}

      - name: Deploy to Fly.io
        run: flyctl deploy --remote-only
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
```

 ### 2. Show an example of a learning outcome you have struggled with and/or would like to re-visit.
> [**Learning outcome...**]  
We decided to used a Dev Branch and push our code there before pushing our final code into main.
Some of us had some issues with git. 

## Feedback
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
