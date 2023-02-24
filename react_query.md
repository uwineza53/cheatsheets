# React Query Library
React Query Library is a library to provide query and state management combined feature for react.
This library makes easy to querying providing user friendly features to react developers.

## Installation
```bash
npm install react-query
```

## What to import & common usage for ReactQueryLibrary
In app.js you have to import QueryClientProvider and QueryClient and wrap it over component require fetching.

```javascript
import React from 'react';
import './App.css';

import { QueryClientProvider, QueryClient } from 'react-query';
import { ReactQueryDevtools } from 'react-query/devtools'
import ReactQuery from './components/ReactQuery';

function App() {
  const queryClient = new QueryClient();
  return (
    <QueryClientProvider client={queryClient}>
      <ReactQuery />
      <ReactQueryDevtools position='bottom-right' />
    </QueryClientProvider>
  );
}

export default App;
```

In fetching components you have to import useQuery.

```javascript

```

## what options are available for react-query
Options makes reactQuery very easy for developper to improve user experience in friendly manner.

1. Cache Time (default is 5 minutes)

```javascript
const { isLoading, data } = useQuery('employeesList', employeesFetch, {
    cacheTime: 5000
  });
```

2. Stale Time
This help to keep request fresh, default is 0 second

```javascript
const { isLoading, data, isFetching } = useQuery('employeesList', employeesFetch, {
    staleTime: 5000
  });
```

3. Refetch

```javascript
const { isLoading, data, isFetching } = useQuery('employeesList', employeesFetch, {
    refetchOnMount: true,
    //refetchOnWindowFocus: true
  });
```

4. Polling 
Refetching events on interval

```javascript
const { isLoading, data, isFetching } = useQuery('employeesList', employeesFetch, {
    refetchInterval: 5000
    // To continuous fetch in background
    refetchIntervalInBackground: true
  });
  ```

5. UseQuery - On Click
When you want to fetch data after click event.

```javascript
const { isLoading, data, isFetching, refetch } = useQuery('employeesList', employeesFetch, {
    enabled: false
});

return (
    <button onClick={refetch}>Load data</button>
)
```

6. Success and Error callback
On Query success you can do something with returned data and also on Query fail you can get access to returned error

```javascript
const onSuccess = (data) => console.log(data)
const onError = (err) => console.log(err.message)
const { isLoading, data, isFetching } = useQuery('employeesList', employeesFetch, {
    onSuccess,
    onError,
  });
```

7. Data transformation

```javascript
const { isLoading, data, isFetching } = useQuery('employeesList', employeesFetch, {
    select: (data) => {
        const employee = data.map(employee => employee.name)
        return employee;
    }
});
```

8. Query by ID

```javascript
const employeeFetch = async ({ queryKey }) => {
    const employeeId = queryKey[1];
    const res = await fetch(`https://jsonplaceholder.ir/users/${employeeId}`);
    return await res.json();
}

//let say id is pass via url, the we use react-router-dom useParam() hook
const { employeeId } = useParams();

const { isLoading, data, isFetching } = useQuery(['employee', employeeId], employeeFetch)
```

9. Parallel Fetch
In parallel fetching works perfect the problem come in when your are going destruct useQuery() property and is using arial names to cop out this issue.

```javascript
const employeesFetch = async () => {
    const res = await fetch('https://jsonplaceholder.ir/users');
    return await res.json();
};

const employeeFetch = async () => {
    const res = await fetch('https://jsonplaceholder.ir/users/1');
    return await res.json();
};


const { data: employeeData } = useQuery('employee', employeeFetch);
const { data: employeesData } = useQuery('employeesList', employeesFetch);
```

10. Dynamic paraller fetching
For Dynamic paraller Query we have to import useQueries instead of useQuery

```javascript
const employeeFetch = async (id) => {
    const res = await fetch(`https://jsonplaceholder.ir/users/${id}`);
    return await res.json();
};

const users = [1, 2, 3];

const queryResults = useQueries(users.map(id => {
    return {
        queryKey: ['employee', id],
        queryFn: () => employeeFetch(id)
    }
}));

console.log({queryResults});
```

11. Dependent Query
```javascript
const employeeEducation = async ({ queryKey }) => {
    const schoolId = queryKey[1] 
    const res = await fetch(`https://jsonplaceholder.ir/users/education/${schoolId}`);
    return await res.json();
};

const employeeFetch = async ({ queryKey }) => {
    const id = queryKey[1] 
    const res = await fetch(`https://jsonplaceholder.ir/users/${id}`);
    return await res.json();
};

const { data: employee } = useQuery(['employee', 1], employeeFetch)

const schoolId = employee?.schoolId;

const { data: education } = useQuery(['school', schoolId], employeeEducation, {
    enabled: !!schoolId
})
```

12. Initial Query Data
This react query feature prevent loading by displaying some of the existing from previous cached query data until current query data is available.

To be able to use it first import, useQueryClient to access the query client that holds previous cached query data. then add initialData option to useQuery()

```javascript
const employeeFetch = async ({ queryKey }) => {
    const employeeId = queryKey[1];
    const res = await fetch(`https://jsonplaceholder.ir/users/${employeeId}`);
    return await res.json();
}

//let say id is pass via url, the we use react-router-dom useParam() hook
const { employeeId } = useParams();

// Todo:
const queryClient = useQueryClient();

const { isLoading, data, isFetching } = useQuery(['employee', employeeId], employeeFetch, 
{
    initialData: () => {
        const employee = queryClient.getQueryData('employees')?.find(employee => employee.id === parseInt(employeeId))

        if (employee)
            // You have to return desired structure
            return employee;
        else
            // You are obliged to return undefined
            return undefined;
    },
})
```