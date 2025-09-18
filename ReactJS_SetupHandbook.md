# React Handbook

## 01 Basic setup

Create vite + react front end

```bash
    npm create vite@latest .
```

Install all dependencies

```bash
    npm install tailwindcss @tailwindcss/vite
    npm i react-router-dom
    npm i @reduxjs/toolkit
    npm i @types/uuid
    npm install react-router-hash-link
```

Add tailwind config to vite.config.js

```javascript
    import { defineConfig } from 'vite'
    import react from '@vitejs/plugin-react-swc'
    import tailwindcss from '@tailwindcss/vite'

    // https://vite.dev/config/
    export default defineConfig({
    plugins: [
        react(),
        tailwindcss(),
    ],
    })
```

Add tailwind to css file App.css

```css
    @import "tailwindcss";
```

Add Fredoka font

Index.html
```html
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&display=swap" rel="stylesheet">
```

App.cs
```css
    :root{
        font-family: Fredoka, ui-sans-serif, system-ui, sans-serif;
    }
```

---

## 02 Approutes setup

Create a folder /src/layout
Create files: Layout.jsx and AppRoutes.jsx

**Layout.jsx**
```jsx
    import { Outlet } from "react-router-dom";

    function Layout() {
        return(
            <div>
                {/* <SideBar/> */}
                <Outlet/>
            </div>
        )
    };

    export default Layout
```

**Approutes.jsx**
```jsx
    import { BrowserRouter, Outlet, Route, Routes } from "react-router-dom";
    import Home from "../pages/home/Home.jsx";
    import SignIn from "../pages/signIn/SignIn.jsx";
    import Dashboard from "../pages/dashboard/Dashboard.jsx";

    function AppRoutes() {
        return(
            <BrowserRouter>
                <Routes>

                    <Route path="/" element={<Home/>} />
                    <Route path="/signin" element={<SignIn/>} />

                    <Route path="/" element={<Outlet/>}>
                        <Route path="/dashboard" element={<Dashboard/>} />
                    </Route>

                </Routes>
            </BrowserRouter>
        )
    };

    export default AppRoutes
```

**App.jsx**
```jsx
    import './App.css'
    import AppRoutes from './layout/AppRoutes.jsx'

    function App() {

    return (
        <AppRoutes/>
    )
    }

    export default App
```

## 03 Links and hash behaviours

Write scrollToTop.jsx to reset scroll to 0,0 when navigating between pages.
Install HashLink package to navigave to sections inside page.

src/components/scrollToTop/ScrollToTop.jsx

**ScrollToTop.jsx**
```jsx
    import { useEffect } from 'react';
    import { useLocation } from 'react-router-dom';

    function ScrollToTop() {
    
    let { pathname, hash } = useLocation();

    useEffect(() => {
        if(!hash){
        window.scrollTo(0, 0);
        }
    }, [pathname, hash]);

    return null;
    }

    export default ScrollToTop
```

Update AppRoutes.jsx

**AppRoutes.jsx**
```jsx
    import { BrowserRouter, Outlet, Route, Routes } from "react-router-dom";
    import Home from "../pages/home/Home.jsx";
    import SignIn from "../pages/signIn/SignIn.jsx";
    import Dashboard from "../pages/dashboard/Dashboard.jsx";
    import WaitingList from "../pages/waitingList/WaitingList.jsx";
    import ScrollToTop from "../components/scrollToTop/ScrollToTop.jsx";

    function AppRoutes() {
        return(
            <BrowserRouter>
                <ScrollToTop /> {/* Reset scroll position to Top of the page  */}
                <Routes>

                    <Route path="/" element={<Home/>} />
                    <Route path="/waitinglist" element={<WaitingList/>} />

                    <Route path="/" element={<Outlet/>}>
                        <Route path="/dashboard" element={<Dashboard/>} />
                    </Route>

                </Routes>
            </BrowserRouter>
        )
    };

    export default AppRoutes

```

**HashLink**

```jsx
    import { HashLink } from "react-router-hash-link"
    <HashLink to="/#pricing">Pricing</HashLink>
```