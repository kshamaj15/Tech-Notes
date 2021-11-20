## connect Redux with any component using  `connect`

```
import React from 'react';
import { connect } from 'react-redux';

const SongList = props => {
    console.log(props); // here prop = mapStateToProps()
    return (
        <h1> SongList </h1>
    );
};

const mapStateToProps = (state) => {
    console.log(state);
    return { songs: state.songs }; // return value will be equal to the props of the component
}

export default connect(mapStateToProps)(SongList);
```

## calling action creator in component

