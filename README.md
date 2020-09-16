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


  
