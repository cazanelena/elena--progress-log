## Guidance
Answer the following questions considering the [learning outcomes for this week](https://learn.foundersandcoders.com/course/syllabus/developer/client-side-app/learning-outcomes/).
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of a learning outcome you have achieved this week.
> **[Learning outcome...]**
> I learned how to use a count state and passed it on as a denpendancy to useEffect in order to render a new set of questions every time the user would click a reset button.

> [your evidence here]

```js

 const [count, setCount] = useState(0);


  useEffect(() => {
    async function initializeTrivia() {
      try {
        const shuffledQuestions = await fetchTrivia(options); // Call the fetchTrivia function
        setQuestions(shuffledQuestions);
        setUserAnswers(shuffledQuestions.map((_) => undefined));
      } catch (error) {
        console.error(error);
      }
    }
    initializeTrivia();
  }, [count, options]);

  const incrementCount = () => {
    setQuestions([]);
    setUserAnswers([]);
    setCurrentQuestionIndex(0);
    setShowQuestions(true);
    setIsHomePage(true);
    setCount(count + 1)
}

```


 ### 2. Show an example of a learning outcome you have struggled with and/or would like to re-visit.
> [**Learning outcome...**]
> Our games ended up having a file with quite a fair bit of states that we were managing. Idealy in the future I would like to learn more how can I refactor my code in a better way and avoid having 7 states in one component.
> [your evidence here]
>
 ```js
function TriviaApp() {
  const [questions, setQuestions] = useState([]);
  const [userAnswers, setUserAnswers] = useState([]);
  const [currentQuestionIndex, setCurrentQuestionIndex] = useState(0);
  const [showQuestions, setShowQuestions] = useState(true);
  const [isHomePage, setIsHomePage] = useState(true);
  const [count, setCount] = useState(0);
  const [options, setOptions] = useState({});
```

## Feedback
> Beth

> Well done getting the hang of useState and useEffect to manage state and side effects in your component. Using the count state as a dependency in the useEffect is a smart way to re-fetch questions whenever the user wishes to reset 👏

> o address the issue of multiple states, you could consider using the useReducer hook, which allows for more complex state logic to be encapsulated in actions and reducers. See here for more: [use reducer](https://react.dev/reference/react/useReducer)


> Elena
>
> Thanks Beth, I am planning to use my consolidation day to work more on react. I love their website, I will have  a look at that. 
