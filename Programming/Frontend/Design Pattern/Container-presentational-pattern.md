- ### Description :
	- separates UI logic from business logic by creating **container components** (handle state and logic) and **presentational components** (focus solely on rendering UI)
- ### Benefits :
	- encourage single-responsibility principle 
	- simplifies component reusability and unit testing
	- facilitates team collaboration by distinguishing responsibilities.
- ### Example :
 ```tsx 
import { useState } from "react";

import PresentationalApp from "./Presentational";

export type ITodo = {

    title: string,

    id: string,

    completed:boolean

}

  

const Container = () => {

    const [todoList, setTodoList] = useState<ITodo[]>([])

    const [todo, setTodo] = useState<string>("");

    const AddTodoListHandler = () => {

        setTodoList([...todoList, { title: todo, id: Math.random().toString(), completed: false }]);

        setTodo("")

    }

    const onClickHandler = (idx:number) => {

        const todos = [...todoList];

        todos[idx].completed = !todos[idx].completed;

        setTodoList(todos);

    }

   return (

     <PresentationalApp

       todo={todo}

       setTodo={setTodo}

       AddTodoListHandler={AddTodoListHandler}

       todoList={todoList}

       onClickHandler={onClickHandler}

     />

   );

}

  

export default Container;

--------------------------------------------------------------------------------------

import {ITodo} from "./Container";

interface IContainer {

  todo: string;

  setTodo: (arg0: string) => void;

    AddTodoListHandler: () => void;

    todoList: ITodo[];

    onClickHandler: (arg0: number) => void;

}

  

const PresentationalApp = ({

  todo,

  setTodo,

  AddTodoListHandler,

  todoList,

  onClickHandler,

}: IContainer) => {

  return (

    <div>

      <input

        type="text"

        value={todo}

        onChange={(e: React.ChangeEvent<HTMLInputElement>) =>

          setTodo(e.target.value)

        }

      />

      <button onClick={AddTodoListHandler}>Submit</button>

      <div>

        {todoList.map((item, idx) => (

          <h1

            onClick={() => onClickHandler(idx)}

            style={{

              textDecoration: item.completed ? "line-through" : "none",

            }}

          >

            {item.title}

          </h1>

        ))}

      </div>

    </div>

  );

};

  

export default PresentationalApp;
 ```