### Description:
A pattern where a component shares logic by providing a function(prop) that controls what to render . The parent component decides how the UI should look.

### Benefits:
- Provides granular control over rendering logic. 
- enable sharing functionality with High order component or hooks
- simplifies scenarios where UI needs to change based on logic

### Example in Real Tools:
- **React Motion:** Uses render props to allow custom animations for components.

**This is the needed component , but here the problem is ==when I want to make same component but with articles or any thing else , here we should use Render Props Pattern==**
``` tsx
import { useEffect, useState } from "react";
export type Posts = {
  userId: number;
  id: number;
  title: string;
  body: string;
};
const PostRendering = () => {
  const [isLoading, setIsLoading] = useState<boolean>(false);
  const [posts, setPosts] = useState<Posts[]>([]);
  useEffect(() => {
    setIsLoading(true);
    fetch("https://jsonplaceholder.typicode.com/posts")
      .then((response) => response.json())
      .then((json) => {
        setPosts(json);
        setIsLoading(false);
      });
  }, []);
    if(isLoading)return <h1>Post is still Loading</h1>
    return <div>
        {
            posts?.map((post, index) => (
                <div key={index}>
                    <h1>{post.title}</h1>
                    <h1>{post.body}</h1>
                </div>
            ))
      }
  </div>;
};
export default PostRendering;
```


**This is an dataFetcher component that allows url and render function , which url refers to api url and render refers to function that return JSX element without needing to Repeat  above component just call DataFetchera and pass to it url link and component as a render function.**
```tsx
import { useEffect, useState } from "react";
import { Posts } from "./PostRendering";
interface IProps {
    url: string,
    render: (data:Posts[], isLoading: boolean) => JSX.Element;
}
const DataFetcher = ({ url, render }: IProps) => {
     const [isLoading, setIsLoading] = useState<boolean>(false);
    const [data, setData] = useState<Posts[]>([]);
     useEffect(() => {
        setIsLoading(true);
        fetch(url)
          .then((response) => response.json())
          .then((json) => {
            setData(json);
            setIsLoading(false);
          });
      }, []);
    return render(data, isLoading);
}
export default DataFetcher;
```


**Here I call DataFetcher and assign url to it and needed component**
```tsx
import DataFetcher from "./DataFetcher";
import { Posts } from "./PostRendering";
const RenderPost = () => {
    return DataFetcher({
        url: "https://jsonplaceholder.typicode.com/posts",
        render(data, isLoading) {
            if (isLoading) return <h1>Post is still Loading</h1>;
            return (
              <div>
                {data?.map((post:Posts) => (
                  <div key={post.id}>
                    <h1>{post.title}</h1>
                    <h1>{post.body}</h1>
                  </div>
                ))}
              </div>
            );
        },
    })
}
export default RenderPost;
```