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

* use Outlet Context to share data through Outlet child routes
first, define context in your outlet
```javascript
    <Outlet context='share information' />
```

next, getting your context data to your child route
```javascript
    import React, { useOutletContext } from 'react';

    const TestPage = () => {
        const outletData = useOutletContext();

        console.log(outletData);
        return (
            ...
        );
    };
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

## Context and useContext
This react native feature make it possible share values through component tree without props drilling.

* Creating context, in new contexts component apart.
```javascript
    import React, { createContext } from 'react';

    export const userContext = createContext('default value');
```

* Defining context provider
```javascript
    import React from 'react';
    import { UserContext } from './UserContext';

    const App = () => {
        <UserContext.Provider value='assigned data'>
            <TestPage />
        </UserContext>
    }

    export default App
```

* Using context
```javascript
    import React, { useContext } from 'react';
    import { UserContext } from './UserContext';

    const TestPage = () => {
        const userContext = useContent(UserContext)

        console.log(userContext)

        return (
            ...
        );
    };

    export default TestPage
```

## Hooks: useState
state refered to mutable data store in certain components

* Definition
```javascript
    const [visit, setVisit] = useState({
        email: 'mulisa@gmail.com',
        visits: 0
    })
```

* Mutating state
```javascript
    const visiting = () => {
        setUser({...visit, visits: visit.visits + 1})
        // OR
        setUser({email: 'kalisa@gmail.com', visits: visit.visits + 1})
    }

    const TestPage = () => {
        return (
            <button onClick={visiting}> + add Visit </button>
        )
    }
    export default TestPage
```

## Hooks: Reducer
The best option over useState is reducers, no need to install imported from react

* Syntax:
```javascript
    const initialState = {
        email: 'kalisa@gmail.com',
        visits: 0
    }

    const reducerFn = (state, action) => {
        switch(action.type) {
            case 'visitIn':
                return {...state, visits: state.visits + 1};
            case 'visitOut':
                return {...state, visits: state.visits - 1};
            default:
                return state
        }
    }

    const [state, dispatch] = useReducer(reducerFn, initialState);

    const TestPage = () => {
        return (
            <button onClick={() => dispatch({type: 'visitIn'})}> + add Visit </button>
        )
    }

    export default TestPage
```

## Hooks: useEffect
use effect hook is use control side effects.

* syntax
```javascript
    // take effect if any deps list changed
    useEffect(callback, [deps]);
    // take effect at initial render (when component mount)
    useEffect(callback, []);
    // take effect on every reload
    useEffect(callback);
```

## Hooks: useMemo
hook used for memoization of long calculation to improve performance

* syntax
```javascript
    const val = useMemo(callback, [deps]);
```

## Hooks: useCallback
hook used for memoization of long computation function to improve performance

* syntax
```javascript
    const fn = useCallback(callback, [deps]);
```