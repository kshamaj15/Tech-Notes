React is the state management library

### Redux cycle
to change state of out project we call an -> `Action creater` -> (creates an) -> `Action` -> gets fed to -> `Dispatch` -> forword the action to -> `Reducer` -> creates new -> `State` -> wait until we need to update our state again

## 1.  action creation
```
const createPolicy = (name, amount) => {
  return {
    type: 'CREATE_POLICY',
    payload: {
      name, amount
    }
  }
}

const deletePolicy = (name) => {
  return {
    type: 'DELETE_POLICY',
    payload: {
      name
    }
  }
}

// action creation
const createPolicy = (name, amount) => {
  return {
    type: 'CREATE_POLICY',
    payload: {
      name, amount
    }
  }
}

const createClaim = (name, amountofMonetToCollect) => {
  return {
    type: 'CREATE_CLAIM',
    payload: {
      name, amountofMonetToCollect
    }
  }
}
```

## 2. Creating the reducers
```

// Reducers
const claimsHistory = (oldListOfClaims = [], action) => {
  if(action.type === 'CREATE_CLAIM') {
    return [...oldListOfClaims, action.payload]
  }
  return oldListOfClaims;
}

const accounting = (currentBagOfMoney = 100, action) => {
  if(action.type === 'CREATE_CLAIM') {
    return currentBagOfMoney - action.payload.amountofMonetToCollect;
  } else if(action.type === 'CREATE_POLICY') {
    return currentBagOfMoney + action.payload.amount;
  }
  return currentBagOfMoney;
}

const listOfPolicies = (listOfPolicies = [], action) => {
  if(action.type === 'CREATE_POLICY') {
    return [...listOfPolicies, action.payload];
  } else if(action.type === 'DELETE_POLICY') {
    return listOfPolicies.filter(poli => poli.name != action.payload.name);
  } 
  return listOfPolicies;
}
```

## 3. Create Store
```
const { createStore, combineReducers } = Redux;

const ourDepartments = combineReducers(accounting, claimsHistory, listOfPolicies);

const store = createStore(ourDepartments);

const action = createPolicy('Alex', 20);
store.dispatch(action);
store.dispatch(createPolicy('Bob', 20));
store.dispatch(createPolicy('Clen', 20));
store.dispatch(createPolicy('Dena', 20));
store.dispatch(deletePolicy('Dena'));
store.dispatch(createClaim('Bob', 50));
console.log(store.getState());
```