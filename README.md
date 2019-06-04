# quiz-tool

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

## How to customize a quiz

Follow the format of `src/quiz.json` to modify the quiz questions and results. The vital structure:

    {
      "title": "Quiz Title",
      "questions": [
        {
          "title": "Question title or prompt",
          "category": "categoryName",
          "answers": {
            "answer": "1",
            "answer": "2",
            "answer": "3",
            "answer": "4"
          }
        }
      ],
      "results": {
        "": {
          "identity": "Result Name",
          "summary": "result description",
          "image": "filename.jpg"
        }
        "categoryName": {
          "identity": "Result Name",
          "summary": "",
          "image": "filename.jpg"
        },
        "categoryName+secondCategory": {
          "identity": "Result Name",
          "summary": "",
          "image": "filename.jpg"
        },
      }
    }

How this works:

Each question earns the user a number of points in its related category. At the end of the quiz, the scores in each category are compared against the maximum possible score. The user's result is based on how many categories they got a "High" score in (at least 75% of the max). 

The app then takes the categories they scored High in, alphabetizeS the category names, and joins them with a `+`. That is why, if the user did not get a High score in ANY category, their result is ""
