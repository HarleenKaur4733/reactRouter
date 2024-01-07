# Interview questions on React Router DOM - Chai aur Code
1. ## Why to not use <a/> tag in react ?
   Because it reloads the entire page, therefore use Link tag.
2. ## Why to use navlink? And why use callback function in navlink?
   Navlink provide us with some additional functionalities including isActive which can be accessed through a call back function.
3. ## How to make a router?
```
ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);

```



```
<li>
                <NavLink
                  to="/"
                  // when we use classname as callback funcnt, we are provided
                  // with a inbuild function isActive

                  className={({ isActive }) =>
                    `block py-2 pr-4 pl-3 duration-200 ${
                      isActive ? "text-orange-700" : "text-gray-700"
                    }  border-b
                                         border-gray-100
                                          hover:bg-gray-50 
                                          lg:hover:bg-transparent 
                                          lg:border-0
                                          hover:text-orange-700 
                                          lg:p-0`
                  }
                >
                  Home
                </NavLink>
</li>
```
3. ### Outlet in react
Header and Footer will remain same on every page, only outlet data will be changed, which make it more optimized
```
const Layout = () => {
  return (
    <>
      <Header/>
      <Outlet/>
      <Footer/>
    </>
  )
}

```

4. ### Use of loader in react?
Optimized technique of fetching data from API or database. It loads data even before useEffect hook.

```
const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<Layout />}>
      <Route path="" element={<Home />} />
      <Route path="about" element={<About />} />
      <Route path="contact" element={<Contact />} />
      <Route path="user/:userid" element={<User />} />
      <Route loader={githubInfoLoader} path="github" element={<Github />} />  // loader is used here
    </Route>
  )
);
```

```
import { useLoaderData } from "react-router-dom";

function Github() {
  const data = useLoaderData();
  // const [data, setData] = useState([]);
  // useEffect(() => {
  //   fetch("https://api.github.com/users/HarleenKaur4733")
  //     .then((response) => response.json())
  //     .then((data) => {
  //       console.log(data);
  //       setData(data);
  //     });
  // }, []);
  return (
    <div className="text-center m-4 bg-gray-600 text-white p-4 text-3xl">
      GitHub followers: {data.followers}
      <img src={data.avatar_url} alt="Git Picture" width={300} />
    </div>
  );
}

export default Github;

export const githubInfoLoader = async () => {
  const response = await fetch("https://api.github.com/users/HarleenKaur4733");
  return response.json();
};

```

