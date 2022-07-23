
# 🎦MY PROJECTS STEPS:
### ➡️Create react app

   
```bash
npx create-react-app my-project-name
cd my-project-name
code .
npm start
```
### ➡️Create necessary components
### ➡️ Install react router
```
 npm install react-router-dom@6
```
### ➡️ go to index.js and wrap App 
```
<BrowserRouter>
      <React.StrictMode>
        <App />
      </React.StrictMode>
    </BrowserRouter>
```
### ➡️ install tailwind
```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```
### ➡️ edit tailwind.config.js file
```
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
### ➡️ copy the code and paste on index.css
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```


## 👌Steps for starting [daisyui](https://daisyui.com/)


- must install tailwind first 
- install ` npm i daisyui`
- go to tailwind.config.js > replace pplug in 
```
 plugins: [require("daisyui")],

 ```
- create custom theme : >go to tailwind.config.js> paste before plugin

```
daisyui: {
    themes: [
      {
        mytheme: {
          primary: "#a991f7",
          secondary: "#f6d860",
          accent: "#37cdbe",
          neutral: "#3d4451",
          "base-100": "#ffffff",
        },
      },
      "dark",
      "cupcake",
    ],
  },
```
- now change primary, secondary according to your



## 👌Steps for React DayPicker [React DayPicker](https://react-day-picker.js.org/)

- install `npm install react-day-picker date-fns`
- import
 ```
     import { DayPicker } from 'react-day-picker';
     import 'react-day-picker/dist/style.css';
 ```
- use in the body ` <DayPicker/>`
- as we need to change time so we'll declare a state and we set the default value as today's date
`  const [date, setDate] = useState(new Date());  ` 


```
                   <DayPicker
                        mode='single'
                        selected={date}
                        onSelect={setDate}
                    />
            
```

- for showing the picked day {format (day,'PP')}

### ➡️ install firebase
```
npm install firebase
```
### ➡️ initialize firebase with given code , copy and paste it in firebase.init.js
### ➡️ import here
```
import { getAuth} from "firebase/auth";
```
### ➡️ create auth and exports default
```
const auth = getAuth(app);
export default auth;
```
### ➡️ install react-firebase-hooks
```
npm install --save react-firebase-hooks
```
### ➡️ install font Awesome
```
npm i --save @fortawesome/fontawesome-svg-core
npm install --save @fortawesome/free-solid-svg-icons
npm install --save @fortawesome/react-fontawesome

```

## 👌Make navbar transparent and when it scrolling give a background
- create a state
```
const [nav, setNav]= useState(true)
```
- declare a function and call it with event listener of scroll 
- if scrollY gather than and equal the nav height setNav(true) else false

```
const changeBackground = () => {
        console.log(window.scrollY);
        if (window.scrollY >= 80) {
            setNav(true)
        }
        else {
            setNav(false)
        }
    }
    window.addEventListener('scroll', changeBackground)

```
- conditionally rendar the style of nav
```
 <nav className={`sticky top-0 h-[80px] ${!nav ? 'bg-transparent' : 'bg-white'} z-50`}>
```

## 🎆Use react reveal for adding animation:
- install
 ``` 
 npm install react-reveal --save
 yarn add react-reveal
 ```
- see their docs [react reveal](https://www.react-reveal.com/examples)

## 🦘Jump a section to another  section on a page by nav
- set a route in the nav
``` <a href='/#section'>section</a> ```
- set the id
``` 
<div id="section">section
</div>
 ```

 ## ⚠️use toast
 ``` yarn add react-hot-toast ```

 - see their docs [React Hot  Toast](https://react-hot-toast.com/)
## 🔐 how to create requiredAuth and how to use
- Create a component named requiredAuth
- code
```
import { Navigate, useLocation } from "react-router-dom";
import auth from "../../firebase.init";

function RequireAuth({ children }) {
    const location = useLocation();
    if (!auth.user) {
        return <Navigate to="/login" state={{ from: location }} replace />;
    }
    return children;
}
export default RequireAuth;
```
- wrap those components in App.js that want to protect.
```
element={<RequireAuth><AddEvent /></RequireAuth>}
```
- redirect after login in 
```
const navigate = useNavigate()
const location = useLocation()
let from = location.state?.from?.pathname || "/"
```

```
const [user, loading] = useAuthState(auth)
    useEffect(() => {
        if (user) {
            navigate(from);
        }
    }, [user]);
```
## 🔃If don't wanna redirect to login page after reload use [user, loading] from useAuthState(auth)

# ➡️ Backend Steps:
### ➡️ create project and initialize
```
mkdir project-name
cd project-name
npm init -y
npm i express mongodb cors dotenv jsonwebtoken
```
### ➡️ create index.js , .env and .gitignore file
### ➡️ wrap in .gitignore
```
/node_modules
.env
```

## Install Dev Dependencies

```
yarn add -D eslint prettier
npx install-peerdeps --dev eslint-config-airbnb-base
yarn add -D eslint-config-prettier eslint-plugin-prettier
```

## Setup Linting Configuration file
Create a `.eslintrc.json` file in the project root and enter the below contents:

```
{
  "extends": ["prettier", "airbnb-base"],
  "parserOptions": {
    "ecmaVersion": 12
  },
  "env": {
    "commonjs": true,
    "node": true
  },
  "rules": {
    "no-console": 0,
    "indent": 0,
    "linebreak-style": 0,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 100,
        "tabWidth": 4,
        "semi": true
      }
    ]
  },
  "plugins": ["prettier"]
}
```

### ➡️ credit scripts in package.js
```
"start": "node index.js",
"start-dev": "nodemon index.js",
```
### ➡️ go index.js and require
```
const express = require('express');
const app = express();
const port = process.env.PORT || 5000;
const cors = require('cors');
require('dotenv').config();
const jwt = require('jsonwebtoken');
```
### ➡️ use middleware
```
app.use(cors());
app.use(express.json());
```
### ➡️ get the root api
```
app.get('/', (req, res) => {
    res.send('Hello dude I am from backend')
})
```
### ➡️ listen all the api
```
app.listen(port, () => {
    console.log('your voice is very sweet.');
})
```
### ➡️ go mongodb , sign in, create cluster, copy user , name and password and wrap it in the .env file
```
USER_NAME=user1
USER_PASS=@password#
```
### ➡️ connect to mongodb
- copy the connect copy 
- paste in root of index of html
- replace password and user from .env
```
const { MongoClient, ServerApiVersion } = require('mongodb');
const uri = `mongodb+srv://${process.env.USER_NAME}:${process.env.USER_PASS}@cluster0.mokim.mongodb.net/myFirstDatabase?retryWrites=true&w=majority`;
const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true, serverApi: ServerApiVersion.v1 });
console.log(uri);
```
### ➡️ We will make our all api in a async function 
### ➡️ call the function
### ➡️ so put all the api in the try
```
async function run(){
  try{
 await client.connect();
 const eventCollection = client.db("volunteer").collection("events");
  }
  finally{

  }
}
run().catch(console.dir)
```
### ➡️ make get api for all myFirstDatabase
```
        app.get('/data', async (req, res) => {
            const query = {};
            const cursor = dataCollection.find(query);
            const data = await cursor.toArray();
            res.send(data)
          })
```
### ➡️Post API : Post a data in mongodb
```
app.post('/volunteers', async (req, res) => {
    const newVolunteer = req.body;
    const result = await volunteerCollection.insertOne(newVolunteer);
    res.send(result);
        });
    };
```

### Delete API : Delete a data from mongodb
```
 app.delete('/data/:id', async (req, res) => {
    const id = req.params.id
    const query = { _id: ObjectId(id) }
    const result = await dataCollection.deleteOne(query)
    res.send(result)
})
```

# CURD in client side
### ➡️ for oparate all api in client side we use axios. so install it
```
npm install axios
```
### ➡️ For get all data:
```
const [data, setData] = useState([])
    useEffect(() => {
        const loadData= async () => {
            const { data } = await axios.get('http://localhost:5000/events')
            setData(data);
        }
        loadData()
    }, [])
```
### ➡️ For post a  data:
- declare a data 
- function call through button
- code 
```
const postData = async () => {
    const proceed = await window.confirm('Are you sure registered?')
    if (proceed) {
        try {
            const { data } = await axios.post('http://localhost:5000/data ', newData)
            console.log(data);
            navigate('/')
            toast.success('Congratulation! registration successful.')
        }
        catch (err) {
         console.log();
        }
    }

}
```
### ➡️ For delete a  data:
```
const handleDelete = async id => {
    const url = `http://localhost:5000/data/${id}`
    const { data } = await axios.delete(url)
}

```


## 🔥🔥Steps for diploy on firebase
### Deploy from the start:
- ```npm install -g firebase-tools```(one time in a computer)
- ```firebase login```(one time in a computer)
- ```firebase init```(one time for each project)
  > - ? Are you ready to proceed? (Y/n)
  > - (*) Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys
  > - existing project
  > - Select project
  > - What do you want to use as your public directory? build
  > - Configure as a single-page app (rewrite all urls to /index.html)? No
  > - Set up automatic builds and deploys with GitHub? No
- ```npm run build```
- ```firebase deploy```

### Deploy after every changes:
- ```npm run build```
- ```firebase deploy```



## 🎯Deploy Server in heroku
### One time for a computer.
**➡️** [Sign up heroku ](https://signup.heroku.com/)

**➡️** install heroku 64 bit from doc 

**➡️** ` heroku login ` 

### One time for each project.
**➡️** `heroku create`
### for every changes.
**➡️** `git add .`

**➡️** `git commit -m "messages"`

**➡️** `git push`

**➡️** `git push heroku main`

**➡️** dashboard >settings>revel config vars> put the .env key and valu

