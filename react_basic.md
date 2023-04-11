# React Basics
In this section we will cover some basic skills in react

## React Routing
steps to follow: 

* react router dom installation
```bash
    npm install react-router-dom
```
* wrapping your app in browser router eg. in index.js
```javascript
    <BrowserRouter>
        <app />
    </BrowserRouter>
```

* defining your routes with route
```javascript
    <Routes>
        <Route path='/test/:id' element={<TestPage />} />
    </Routes>
```

* wrapping routes inside global route
first, 
```javascript
    <Routes>
        <Route path='/' element={<WrapperPage />}>
            <Route path='/test/:id' element={<TestPage />} />
        </Route>
    </Routes>
```
next, WrapperPage.js
```javascript
    return (
        <>
            WrapperPage
            { <Outlet /> } //imported from react-router-dom
        </>
    )
```

* Route to match random page (404 page) to handle wrong url linking
```javascript
    <Route path='*' element={<Page404 />} />
```

## React Error Boundary
To handle error in react you can use ErrorBoundary

* ErrorBoundary installation
```bash
    npm install react-error-boundary
```

* importing ErrorBoundary
```javascript
    import { ErrorBoundary } from 'react-error-boundary'
```

* Wrapping Component inside error-boundary
first, 
```javascript
    import React from 'react'

    const ErrorBounds = ({ error, resetErrorBoundary }) => {
        return (
            <div> 
                {error.message}
            </div>
        )
    }

    export default ErrorBounds
```

next,
```javascript
    <ErrorBoundary FallbackComponent={ErrorBounds} 
    OnError={} OnReset={}>
        <MyPage />
        ...
    </ErrorBoundary>
```
