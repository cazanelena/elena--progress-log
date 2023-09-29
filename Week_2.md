## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/database/learning-outcomes/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.
 - GitHub Actions CI setup to run your tests when you push
   <img width="659" alt="Screenshot 2023-09-28 at 16 00 00" src="https://github.com/fac28/elena--progress-log/assets/59057287/f4ab229c-27e5-455c-b1b5-57475a30936f">


> **[Learning outcome...]**  

Yml file below:
 
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

We decided to used a Dev Branch and push our code there before pushing our final code into main.
Some of us had some issues with git such as their branch was ahead of the original branch, or accidentally merged code into main and ending with some code in the dev branch and some in main. I would like to learn more about how to set up some rules in github that will prevent us from making this mistakes in the future. 

I did some research and found some interesting articles about best practices using git.
Links here: 
https://medium.com/git-happy/10-key-best-practices-for-git-branch-management-b0e7ec4148b9

https://www.gitkraken.com/learn/git/best-practices/git-branch-strategy


I also came accross GitHub release which can potentially be a good alternative to keep your code clean, and make sure that your app is always working as expected. 

**GitHub Releases** is a feature provided by GitHub that allows you to package and distribute specific versions of your software or project to your users or collaborators. It is a way to formally publish and distribute your project's releases, making it easier for others to understand what changes have been made in each release and to access the associated assets and documentation.

https://github.com/marketplace/actions/create-github-release


## Feedback
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
