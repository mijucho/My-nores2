# My-note2

## Wk5 -API
App.jsx
```
import React from 'react'
import Urban from './Urban' 
import { getDefinition } from '../api/urban';



class App extends React.Component {

  constructor(props) {
    super(props)

    this.state = {
      name : null
    }

    this.handleChange = this.handleChange.bind(this)
    this.loadDefinition=this.loadDefinition.bind(this)
  }


  handleChange(event){
    this.setState({ name: event.target.value })
  }


  loadDefinition(){
    return getDefinition(this.state.name)
    .then((data) => {this.setState({name:data})})
  }


  render(){
  return (
    <React.Fragment>
    <Urban name={this.state.name} />
    <form onSubmit={event => event.preventDefault()}>
       <label><input type="text" name="text" onChange={this.handleChange}/></label>
       <button onClick={this.loadDefinition}>Submit</button>
    </form>
    </React.Fragment>
  )
  }
}

export default App
```
Urban.jsx
```

import React from 'react'

class Urban extends React.Component {
  constructor(props) {
    super(props)

  }

  render () {
    return(
    <div>
      {this.props.name && (
        <div>
          <h2>{this.props.name.word}</h2>
          <p>Definition: {this.props.name.definition}</p>
          <p>Example: {this.props.name.example}</p>
        </div>
        )}
     
    </div>
    )
  }
}

export default Urban
```
api/urban.js
```
import request from 'superagent'
const apiEndpoint = ("https://mashape-community-urban-dictionary.p.mashape.com/define?term=")

export function getDefinition(name) {
  return request 
  .get(apiEndpoint + name).set('x-mashape-key', 'IUU7GyrOK4mshNOCbJEmBmj5SKSop1kSmPJjsn2nWIxgxzZbEc').then(res => {
    return res.body.list[0]
  })
}
```
