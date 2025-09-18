# Express JS Handbook

## 01 Basic setup

Create node + express js backend.

```bash
    npm init
    npm i express
    npm i cors
```

Create server.js, update package.json and create one route.

**server.js**
```js
    import express from "express";
    import cors from "cors";
    import waitingListRouter from "./routes/marketing/waitingListRouter.js";

    const server = express();

    server.use(express.json());

    server.use(cors());

    let port = 8000;

    server.get("/", (req,res)=>{
        res.send({code:1, msg:"Quwad Backend"})
    });

    // Routes
    server.use("/waitinglist", waitingListRouter);


    // Server Listen
    server.listen(port, ()=>{
        console.log(`Server running on port ${port}`);
    });
```

**package.json**
```js
    {
    "name": "backend_quwad",
    "version": "1.0.0",
    "description": "",
    "main": "server.js", // update this line
    "type": "module", // add this line
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "server": "node --watch server.js" // add this line
    },
    "author": "",
    "license": "ISC",
    "dependencies": {
        "cors": "^2.8.5",
        "express": "^5.1.0"
    }
    }

```

Create folder routes/marketing/waitingListRouter.js

**WaitingListRouter.js**
```js
    import express from "express";

    let waitingListRouter = express.Router();

    waitingListRouter.get("/", async (req, res)=>{
        
        let body = req.body;

        console.log(body)

        // Create a record in waiting list collection

        // Send response
        res.send({code:1, msg:"Successfully joined waiting list."})
    });

    export default waitingListRouter
```