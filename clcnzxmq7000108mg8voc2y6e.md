# How to implement an API fetch of your GitHub portfolio

An API, or application programming interface, is a set of guidelines and standards for accessing a web-based software application or web tool. One of the most popular APIs for developers is the GitHub API, which allows users to access and retrieve data from their GitHub portfolio. In this article, I'll show you how to implement an API fetch of your GitHub portfolio using a few simple steps.

This tutorial is geared towards developers who are familiar with programming concepts and have some experience with using APIs. Whether you're looking to display your GitHub projects on your personal website or create a custom tool to analyze your code, learning how to fetch your GitHub portfolio through the API can be a useful skill to have in your developer toolkit.

The live demo of this application is available [here](https://annietah-repos.netlify.app/). Here’s the [source code](https://github.com/Anita9771/second_semester_exam) for the project.

You can get the styles and images used in this project from [here](https://github.com/Anita9771/second_semester_exam.git).

### Prerequisites

To complete this project, you will need some knowledge of the following

* Adequate knowledge of [React](https://reactjs.org/)
    
* Node and its package manager, `npm`. Run the command `node -v && npm -v` to verify that you have them installed or install them from [here](https://nodejs.org/en/)
    
* [Code Editor](https://code.visualstudio.com/)
    
* Experience using APIs
    
* A GitHub account and at least one repository
    

> NOTE: To get you started, the prerequisites are attached with links to guide you. You can also catch up with crash courses.

### What is GitHub API?

The GitHub API is a way for programs to interact with GitHub. It provides a way for developers to fetch data from and interact with the GitHub platform, such as by retrieving a list of repositories for a particular user or creating a new repository.

The API is accessed using HTTP and is available in a number of different programming languages. It is often used to automate tasks, integrate with other tools and platforms, and build custom applications on top of GitHub.

# Getting Started

* Create a react application by running the command `npx create-react-app app-name`
    
* Navigate to the `app-name` directory and run `code .` to open it on your VSCode
    
* Install `react-router-dom`, `react-helmet`, and `react-spinners` as you'll be using these in this project
    

### Project Setup and Installation

Ensure you have an `assets`, `components` and, `pages` folder in your project.

In your `pages` folder, create five files namely `GithubList.js`, `GithubPage.js`, `HomePage.js`, `Services.js`, and `Index.js`.

In your `components` folder, create five files namely `Error404.js`, `ErrorBoundary.js`, `HomeNav.js`, `Pagination.js`, and `Index.js`.

Your `App.js` should contain the following imports and routes for navigation.

`App.js`

```javascript
import './App.css';
import { useState } from 'react';
import {BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import { Error404, ErrorBoundary, HomeNav } from './components';
import { GithubList, GithubPage, HomePage, Services } from './pages';

function App() {

  return (
    <div className="App">
       <Router>
        <HomeNav />
        <Routes>
          <Route path='/' element={<HomePage />} /> 
          <Route exact path='/repositories' element={<GithubList />} /> 
            <Route exact path='repositories/:repoId' element={<GithubPage />} />
          <Route path='/services' element={<ErrorBoundary><Services /></ErrorBoundary>} />
          
          <Route path='/*' element={<Error404 />} /> 
        </Routes>
      </Router>
    </div>
  );
}

export default App;
```

In your `components` folder

`Index.js`

```javascript
export {default as HomeNav} from './HomeNav'
export {default as Error404} from './Error404'
export {default as ErrorBoundary} from './ErrorBoundary'
export {default as Pagination} from './Pagination'
```

This is to get all files of the folder in one place for easy export during the project.

`HomeNav.js`

```javascript
import React from "react";
import { Link } from "react-router-dom";
import GithubLogo from "../assets/images/github-logo.png";
import "./styles.css";


const HomeNav = () => {
  
  return (
    <nav className="home-nav">
        <Link className="link" to='/'><h2>ZOOL</h2></Link>
      
      <ul>
        <Link to='/' className="link"><li>Home</li></Link>
        <Link to='/repositories' className="link"><li>Repositories</li>      </Link>
        <Link to='/services' className="link"><li>Services</li></Link>
      </ul>
      <div className="logo">

        <a href='https://github.com/Anita9771/' target="_blank" ref="noreferrer"><img src={GithubLogo} alt="github logo" /></a>
      </div>
    </nav>
  );
};

export default HomeNav;
```

The `HomeNav.js` component will serve as the top navigation bar. Your navbar should look like this after implementing the `HomeNav`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673205243390/21210d7f-b8ea-43c2-8c7f-e6afb9ae127a.png align="center")

`ErrorBoundary.js`

```javascript
import React, { Component } from 'react';
import { Link } from 'react-router-dom';
import './styles.css'
export class ErrorBoundary extends Component {

  constructor(props) {
    super(props)
  
    this.state = {
       error: null,
    }
  }

  componentDidCatch(error, errorInfo){
    console.log({error, errorInfo});
  }

  static getDerivedStateFromError(error){
    return {error};
  }
  

  render() {
    if(this.state.error)
    return <div className='error-boundary'>Oops! Something went wrong!
    <Link className='link' to='/'>GO HOME</Link>
    </div>;

    return this.props.children;
  }
}

export default ErrorBoundary;
```

In the above component, you introduced [error boundary](https://reactjs.org/docs/error-boundaries.html) which will help to catch errors during development. You'll use this in the `Services.js`, a page added for this purpose.

`Error404.js`

```javascript
import React from 'react'
import { Link } from 'react-router-dom'
import ErrorPage from '../assets/images/error.gif'

const Error404 = () => {
  return (
    <div style={{color: 'white'}} className="error-page">
      <img style={{width: '10rem', height: '10rem', borderRadius: '2rem'}} src={ErrorPage} alt="error -page" />
        <h1>404</h1>
        <h2>This page cannot be found. <br /> Please, check your URL.</h2>
        <Link className="link" to='/'>GO HOME</Link>
    </div>
  )
}

export default Error404
```

The above component is the defined UI for a [404 page](https://www.atlassian.com/blog/statuspage/error-pages). The outcome should look like this

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673218578472/5f9e8475-9508-444a-9827-b6c0a559479a.png align="center")

`Pagination.js`

```javascript
import React from "react";

const Pagination = ({ reposPerPage, totalRepos, paginate, currentPage }) => {
  const pageNumbers = [];

  for (let i = 1; i <= Math.ceil(totalRepos / reposPerPage); i++) {
    pageNumbers.push(i);
  }

  return (
    <nav>
      <div
        className="pagination"
        style={{ display: "flex", justifyContent: "space-around" }}
      >
        {pageNumbers.map((number) => (
          <section key={number}>
            <button
              onClick={() => paginate(number)}
              disabled={currentPage === number}
            >
              {number}
            </button>
          </section>
        ))}
      </div>
    </nav>
  );
};

export default Pagination;
```

You'll use this in the `GithubList.js` page to scroll between pages of the repositories.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673206696836/c6c14c55-0e91-4855-91eb-d69232b8dd9f.png align="center")

> NOTE  
> At the top of all your pages, it is important to import `react-helmet` as this helps with our Search Engine Optimization (SEO).

At the top of all files created in the `pages` folder, using this format from `GithubList.js` add `react-helmet` to all files.

`GithubList.js`

```javascript
import { Helmet } from "react-helmet"

const GithubList = () => {
  return (
      <Helmet>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1"/>
        <meta
          name="keywords"
          content="seo, 404, error boundary, github API, repositories,               repository, zool, altschool, exam, second semester"
        />
        <meta
          name="description"
          content="Implement an API fetch of your GitHub portfolio, show a page with a list of all your repositories on GitHub(the page should implement pagination for the repo list), and create another page showing data for a single repo clicked from the list of repos using nested routes while using all the necessary tools in react. Implement the proper SEO, Error Boundary (show a page to test the error boundary) and 404 pages. Good UI and Designs are important."
        />
        <title>ZOOL</title>
      </Helmet>
      
  );
};

export default GithubList;
```

Do the above for all files in the `pages` folder.

`pages` &gt; `Index.js`

```javascript
export {default as GithubList} from './GithubList'
export {default as GithubPage} from './GithubPage'
export {default as HomePage} from './HomePage'
export {default as Services} from './Services'
```

`HomePage.js`

```javascript
import React from "react";
import ReactLogo from "../assets/images/react-logo.png";
import "./styles.css";
import { Helmet } from "react-helmet";

const HomePage = () => {
  return (
    <div className="homepage">
      <Helmet>
        //helmet content
      </Helmet>
      <div className="homepage-contents">
        <div className="left homepage-content">
          <h1>
            Github <br /> API
          </h1>
          <p>&#9734;&#9734;&#9734;&#9734;&#9734;</p>
          <button>
            <a className="btn" href="https://docs.github.com/en/rest">
              MORE
            </a>
          </button>
        </div>
        <div className="middle homepage-content">
          <p>&</p>
        </div>
        <div className="right homepage-content">
          <img src={ReactLogo} alt="react logo" />
        </div>
      </div>

      <div className="bottom">
        <p>Create integrations, retrieve data, and automate your workflows.</p>
      </div>
    </div>
  );
};

export default HomePage;
```

The `HomePage` should look like this;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673218689418/d17926fb-6b9d-4c03-9682-1d1f7a85fe36.png align="center")

`GithubPage.js`

```javascript
import React, { useEffect, useState } from "react";
import { Link, useParams } from "react-router-dom";
import PulseLoader from "react-spinners/PulseLoader";
import { Error404 } from "../components";
import { Helmet } from "react-helmet";
const GithubPage = () => {
  const [reposId, setReposId] = useState([]);
  const [loading, setLoading] = useState(false);
  const [reposDesc, setReposDesc] = useState(null);
  const params = useParams();
  const { repoId } = params;

  useEffect(() => {
    const fetchRepo = async () => {
      setLoading(true);

      const res = await fetch(`https://api.github.com/repositories/${repoId}`);
      const data = await res.json();
      setReposId(data);

      setLoading(false);
    };

    fetchRepo();
  }, []);

  return (
    <div className="github-page">
 <Helmet> //helmet content </Helmet>
{loading ? (
        <>
          <PulseLoader
            loading={loading}
            size={100}
            color="#fff"
            className="loader"
            aria-label="Loading Spinner"
            data-testid="loader"
          />
        </>
      ) : (
        
          reposId.name === reposDesc ? <Error404 /> : <h1 style={{ color: "white" }}>{reposId.name}</h1>
        
      )}

      {reposId.description === reposDesc ? (
        <h4 style={{ color: "white" }}>
          There is no description for this repository
        </h4>
      ) : (
        <h4 style={{ color: "white" }}>{reposId.description}</h4>
      )}
      <i>{reposId.html_url}</i>
      <Link className="link" to="/repositories">
        Go Back
      </Link>
    </div>
  );
};

export default GithubPage;
```

In the above, the GitHub API for repositories (https://api.github.com/repositories/${repoId}) with dynamic rendering of each repository's details is used.

`GithubList.js`

```javascript
import React, { useState, useEffect } from "react";
import { useNavigate } from "react-router-dom";
import PulseLoader from "react-spinners/PulseLoader";
import { Pagination } from "../components";
import { Helmet } from "react-helmet";

const GithubList = () => {
  return (
    <Helmet> //helmet content </Helmet>
{loading ? (
        <>
          <PulseLoader
            loading={loading}
            size={100}
            color="#fff"
            className="loader"
            aria-label="Loading Spinner"
            data-testid="loader"
          />
        </>
      ) : (
        <ul className="repos">
          {currentRepos.map((repo) => (
            <div key={repo.id}>
              <li><h3>{repo.name}</h3></li>
              <p>{repo.description}</p>

              <button onClick={() => navigate("/repositories/" + repo.id)}>
              &rarr;
              </button>
              <hr />
            </div>
          ))}
        </ul>
      )}
      <div className="paginate">
        <button
          disabled={currentPage <= 1}
          // aria-disabled={page <= pages}
          onClick={() => setCurrentPage((prev) => prev - 1)}
        >
          Prev
        </button>
        <Pagination
          reposPerPage={reposPerPage}
          totalRepos={repos.length}
          paginate={paginate}
          currentPage={currentPage}
        />
        <button
          disabled={currentPage >= lastPage}
          // aria-disabled={currentPage >= indexOfLastRepo}
          onClick={() => setCurrentPage((prev) => prev + 1)}
        >
          Next
        </button>
      </div>
      <section style={{textAlign: "right", marginRight: "20%"}}>
      {currentPage} of {lastPage}
      </section>
    </div>
);
};

export default GithubList;
```

The above code displays the repository according to the number of repository set to be displayed per page.  
This is where you import the `Pagination.js` from earlier on.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673218952373/55b41a4e-9be8-4a67-bad8-7a3d827e1d22.png align="center")

OnClick of the arrow, the repository details are displayed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673218974907/ac19146e-d844-4c20-b708-793edd58beb4.png align="center")

`Services.js`

```javascript
import React from 'react'
import {Helmet} from 'react-helmet'

const Services = () => {
    

    throw new Error();

  return (
    <div className="services">
        Services
    </div>
  )
}

export default Services
```

The `Services.js` page is to implement the `ErrorBoundary.js` component.  
If implemented rightly, it should look like this on any page an error is thrown.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673206923927/2143d1c6-23b8-48e7-ac88-fbc8b9f87838.png align="center")

## Conclusion

In this tutorial, you've retrieved data from your GitHub portfolio using the GitHub API, defined a UI for a 404 page, and implemented an error boundary. With this knowledge, you can build custom tools and applications that make use of your GitHub data.