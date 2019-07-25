# Simple Redux Setup

1. Create redux folder in scr/
2. Create store file within `src/redux`
```javascript
import { createStore, combineReducers } from "redux";
import reducerOne from "./reducerOne";
import reducerTwo from "./reducerTwo";

const reducer = combineReducers({
reducerOne: reducerOne,
reducerTwo: reducerTwo
});
const store = createStore(reducer);

    export default store;
```

3. Create reducer file within `src/redux`
```javascript
// initialize your initial state
const initialState = {
    info: null,
}

// create variables for switch case/action creators
const UPDATE_INFO = 'UPDATE_USER';

// Create your reducer and make sure to have default case
export default function reducer(state=initialState, action){
    switch(action.type){
        case UPDATE_INFO:
        return {...state, info: action.payload}
        default: 
        return state
    }
}

// Create functions to update state
export function updateInfo(newInfo){
    return {
        type: UPDATE_INFO,
        payload: newInfo
    }
}
```

6. Navigate to src/index.js
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
// Import the provider and store you created
import {Provider} from 'react-redux';
import store from './ducks/store';

// Wrap App with Provider and send it a store prop
const render = () => {
  ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>,
document.getElementById('root')
)};
```

5. Choose component to connect to
```javascript
    import React from 'react';
    import {connect} from 'react-redux';
    import {updateInfo} from '../../ducks/reducer'

    class random extends Component {
        // this.props.info => access redux state
        // this.props.updateInfo => access function to 
        // update redux state
        ...
    }

    const mapStateToProps = (reducer) => {
        info: reducer.reducerOne
    }
    const mapDispatchToProps = {
        updateInfo
    }

    export default connect(mapStateToProps, mapDispatchToProps)(random)
```