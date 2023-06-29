# Summarizer App

I have built the Summarizer App using an API from RapidAPI in conjunction with OpenAI. This application allows users to summarize articles and gain quick insights. Throughout the development process, I followed these steps:

## Setting up the Project: 
I started by setting up a ReactJS project using Vite to kickstart the development process.

## Creating a Beautiful UI/UX: 
I designed a responsive and visually appealing user interface using Tailwind CSS. I incorporated a touch of glass morphism to enhance the overall look and feel of the application. For the UI components, I utilized assets such as the link icon, loader, tick, and copy icons.

## Making Advanced RTK Query API Requests: 
I integrated the useLazyGetSummaryQuery hook from the article service to make advanced RTK query API requests. This allows the application to fetch article summaries based on the provided URL.

```javascript
// Code snippet for making API request using useLazyGetSummaryQuery
const handleSubmit = async (e) => {
  e.preventDefault();

  const { data } = await getSummary({ articleUrl: article.url });
}

```


## Managing State with Redux: 
To handle global state management, I leveraged Redux and its associated toolkit. I created a Redux store using configureStore and included the articleApi reducer from the article service. This allows for efficient management of API-related state and actions.

```javascript
// Code snippet for configuring Redux store
import { configureStore, getDefaultMiddleware } from "@reduxjs/toolkit";
import { articleApi } from "./article";

export const store = configureStore({
  reducer: {
    [articleApi.reducerPath]: articleApi.reducer
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(articleApi.middleware)
});

```

## Saving History with Local Storage: 
To enhance user convenience, I implemented local storage functionality. The application stores the user's articles history using the localStorage API. Whenever the app loads, it retrieves the stored articles and updates the allArticles state.

```javascript
// Local storage functionality for storing and retrieving articles history
import React, { useState, useEffect } from 'react';

const Demo = () => {
  const [article, setArticle] = useState({
    url: '',
    summary: '',
  });

  const [allArticles, setAllArticles] = useState([]);

  useEffect(() => {
    const articlesFromLocalStorage = JSON.parse(
      localStorage.getItem('articles')
    )

    if (articlesFromLocalStorage) {
      setAllArticles(articlesFromLocalStorage)

      localStorage.setItem('articles', JSON.stringify(updatedAllArticles))
    }
  }, []);

  // ... component code
}

export default Demo;


```

## Handling Form Events and Error Catching: 
I implemented form event handling to capture the user's input and trigger the summary retrieval process. In case of any errors during the API request, I display an error message to the user.

```javascript
// Form event handling and error message display
import React, { useState, useEffect } from 'react';
import { useLazyGetSummaryQuery } from '../services/article';

const Demo = () => {
  const [article, setArticle] = useState({
    url: '',
    summary: '',
  });

  // ... component code

  const handleSubmit = async (e) => {
    e.preventDefault();

    const { data } = await getSummary({ articleUrl: article.url});

    if (data?.summary) {
      const newArticle = { ...article, summary: data.summary};

      const updatedAllArticles = [newArticle, ... allArticles]; 

      setArticle(newArticle);
      setAllArticles(updatedAllArticles);
    }
  };

  // ... component code
}

export default Demo;


```

## Implementing Copy to Clipboard: 
To facilitate easy sharing and usage of the article summaries, I implemented the handleCopy function. This function allows users to copy the article URL to their clipboard with a single click. The copied URL is indicated by showing the copied icon.

## Writing Clean Code: 
Throughout the development process, I focused on writing clean and maintainable code. This includes organizing the code into reusable components, following best practices, and ensuring code readability.

---

_**The Summarizer App provides a powerful tool for summarizing articles, showcasing my expertise in front-end development, and delivering a seamless user experience. Feel free to explore and utilize the application for summarizing articles effectively.**_
