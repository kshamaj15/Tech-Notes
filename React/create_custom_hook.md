## Custom hook for state persisting in localstorage
`useLocalStorage.js`
```
import { useEffect, useState } from 'react';

const setInLocalStorage = (key, val) => {
    localStorage.setItem(key, JSON.stringify(val));
}

const getSavedValue = (key, intitialValue) => {
    const val =  JSON.parse(localStorage.getItem(key));
    if(val) return val;

    if(intitialValue instanceof Function) return intitialValue();
    return intitialValue;
}

const useLocalStorage = (key, intitialValue = null) => {
    const [value, setValue] = useState(() => {
        return getSavedValue(key, intitialValue);
    });

    useEffect(() => {
        setInLocalStorage(key, value);
    }, [value])

    return [value, setValue];
}

export default useLocalStorage;
```

## Custom hook for consoling prev and current state change after updation
`useUpdateLogger.js`
```
import { useEffect } from "react";

const useUpdateLogger = (value) => {
    useEffect(() => {
        console.log('Updated', value);
        return () => console.log('Prev', value);
    }, [value])
}

export default useUpdateLogger;
```

## Using the hooks
```
import './App.css';

import useLocalStorage from './cutomHooks/useLocalStorage';
import useUpdateLogger from './cutomHooks/useUpdateLogger';

const App = () => {
  const [inputVal, setInputVal] = useLocalStorage('name', () => '');

  useUpdateLogger(inputVal);

  return (
    <div>
      <input 
        type="text" 
        value={inputVal} 
        onChange={(e) => setInputVal(e.target.value)}/>
    </div>
  );
}

export default App;
```
