# Reactjs-using-Firebase-CRUD
It is a React.js CRUD project using firebase .

## 1. At first create a React.js project

```cmd
npx create-react-app my-app
cd my-app
npm start

```

## 2. Go to Firebase console and create a Project and give him a name (ex- student-management)
  - select Add Firebase to your app from realtime database
  - Give the app name then register that name and click Register the app
  - In the next page copy the [<script> code </script>] code under the script 
  - paste that code inside the react .js src folder which name is firebase.js
  - install in cmd > npm i -s firebase
  - import the package into firebase.js 
  >import * as firebase from "firebase";
  
## 3. Create a folder name -components and also two file name: Contactform.js and Contacts.js
- use the bootstrap javascript codes and css code and paste on Public> index.html
- to use the Contactform.js file in to Contact.js file use **import ContactForm from "./Contactform";*
- Build your UX design like input form , radio button ,dropdown button just like normal bootstrap code 

**Initial the values into Const ContactForm*
```javascript
   const ContactForm= (props) =>{
    const initialFieldValues={
        fullName:"",
        mobile:"",
        email:"",
        details:"",
        skills:"",
        gender:""
    }
    var [values,setValues] = useState(initialFieldValues)


```
- assign the name of the input value as you write the initialFieldValues like = **name="fullName"** ,value is must be describe in `{}` this type of brackets **value={values.fullName}** and also create `onChange ` 
```input
<input type="text" class="form-control" placeholder="Full Name" name="fullName" value={values.fullName} onChange={handleInputChange}/>

```

- Create a triger const who work for onChange method 
```javaScript
const handleInputChange = e =>{
        var{name,value}=e.target
        setValues({
            ...values,
            [name]:value
        })
    }


```


- also create `onSubmit` event to submit your data on your form `onSubmit={handleFormSubmit}`
- define that function 
```javascript

  const handleFormSubmit= e=>{
        e.preventDefault();
        props.addOrEdit(values)
    }
```

- all the firebase related work on addOrEdit function which is in Contacts.js
```javascripts
 const addOrEdit=obj =>{
        firebaseDB.child('contacts').push(
            obj,
            err=>{
                if(err)
                console.log(err)            
            }
        )
    }
```
- create a var variable on firebase.js who store the all script file and export it 

```javascript
 var fireDB=firebase.initializeApp(firebaseConfig);

 export default fireDB.database().ref();
```

- import that firebaseDb from firebase in Contact.js page

```javascript
import firebaseDB from "../firebase";
```

- now your add data is done

# Update the data 

## 1. there is two step in this step 1st fetch the value from firebase and update it 
- i. for fetch the value at firse you import `{useState,useEffect}` 
- ii. define a state property 
```javascript
var[contactObjects,setContactObjects]=useState({})
```

-iii. and a callback function 

```javascript
useEffect(()=>{
    firebaseDB.child('contacts').on('value',snaoshot=>{
        if(snaoshot.val()!=null)
        setContactObjects({
            ...snaoshot.val()
        })
    })

},[])

```
just like this 
- iv. Create a table to show the values 
```
<table className="table table-borderless table-stripped">
                    <thead className="table-light">
                        <tr>
                            <th>Full Name </th>
                            <th>Mobile </th>
                            <th>Email </th>
                            <th>Details </th>
                            <th>Skills </th>
                            <th>Gender </th>
                            <th>Action </th>
                        </tr>
                    </thead>
                    <tbody>
                        {
                            Object.keys(contactObjects).map(id=>{
                                return<tr key={id}>
                                    <td >{contactObjects[id].fullName}</td>
                                    <td >{contactObjects[id].mobile}</td>
                                    <td >{contactObjects[id].email}</td>
                                    <td >{contactObjects[id].details}</td>                                   
                                    <td >{contactObjects[id].skills}</td>
                                    <td >{contactObjects[id].gender}</td>
                               
                                 
                                </tr>
                            })
                        }
                    </tbody>
                </table>
```
here use `map` function for using loop and `keys` using for unic identify the objects


- Create a new State variable to hand data 
```javascript
var [currentId,setCurrentId] = useState('')
```
- Create a edit button on table 
```javascript
   <td>
       <a className="btn btn-prymary" onClick={() => {setCurrentId(id)}} >
          <i className="fas fa-pencil-alt"></i>
         </a>
                                        
       </td>
```
onclick button on pencil button use for pass the value with `setCurrentId(id)` parameter id
- in the same time we need to retrive the data on and put it on the from 
```javascript
<ContactForm {...({addOrEdit,currentId,contactObjects})}  />
```
