
# Learn With Me: AirBnb Clone

## Creating The Environment

Access your terminal and enter

```typescript
npx create-next-app --typescript 
```

Choose a name for your project. In my case, I will name it 

```bash
? What is your project named? › my-airbnb-clone
```

Select Yes/No for the following: 

```typescript
? Would you like to use ESLint with this project? › No / [Yes]
```

To achieve a seamless and adaptable design, we are utilizing the client component Tailwind CSS.

```typescript
? Would you like to use Tailwind CSS with this project? › No / [Yes]
```

Select no for src/ directory. 

```typescript
? Would you like to use `src/` directory with this project? › [No] / Yes
```

We have opted for the experimental directory as we will be utilizing the latest app router for this project. 

```typescript
? Would you like to use experimental `app/` directory with this project? › No / [Yes]
```

When prompted for an import alias, simply pressing the enter key will set the default alias to the '@' sign.

```typescript
? What import alias would you like configured? › @/*
```

Please wait for a moment, as you will observe the installation of packages and the creation of your next.js folder.

```typescript
Run `npm audit` for details.
Initialized a git repository.

Success! Created my-airbnb-clone at /Users/yourfolder/my-airbnb-clone
```

Next, open a new file in VSCode by selecting the project folder you just named. 

Now you will see your new structure in your app folder 

<img src = https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExMDcyOWI0NmJhZmViNjkxMThhZmRkM2Q2OThhNTM4NGMwODMwNWMxZCZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/J4JPOMcD6JDBcdsMYo/giphy.gif>

Rather than our typical naming convention of using an underscore for app and document, we now have a singular file named layout.tsx. Also, the usual `index.tsx` has been replaced with the `page.tsx` file. 

Let's return to our terminal.

Run the command to initiate the project.
```
npm run dev 
```
Then, in your browser, navigate to localhost:3000 to access the new app. 
 
You will be greeted with the Next.js 13 welcome screen.

Now let's clean this up! 

Go into your layout.tsx and change your metadata.

<img src = https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExZDUxZjU4YTE0MTA2OWNjYzE5YjhiOTljZWEzOWFjMDc1OTEzZTRiMyZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/9i5nlQmCTaFpepbrEo/giphy.gif>

Please remove any imports above the global.css import.

The only code in your page.tsx should be the following. 

```typescript
export default function Home() {
  return (
    <div> Welcome To My Airbnb Clone!</div>
  )
}
```

Refresh your localhost and you will notice that the tab name in your browser and your page has been updated.

![img](https://i.imgur.com/SfL9Jo8.png)


Now, let's install the font package so that you can change the font easily. 

At the top of layout.tsx, go ahead and input: 

```typescript
import { Nunito } from 'next/font/google' 
```

Now create a constant with a subset that will hold the specific font. 

```typescript
const font = Nunito({
  subsets: ["latin"],
})
```

What this does now is expose the classname which we can give to our body element below.

<img src=https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExNzNlNGY4YWU4NzBjYmZlMjI3ZWQ4OTBlZTAwMWU4NTQzYzVkYmIzNiZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/vIFt94mUPh7HqwNX7L/giphy.gif>

Refresh the localhost and you should see your font has now changed. 

The newer version of Next.js 13 automatically installs tailwind css. So we'll need to remove some premade components. 

First let's clear everything in globals.css page except for the tailwind css directives: 

```typescript
@tailwind base;
@tailwind components;
@tailwind utilities;
```

then go into tailwind.config.js and ensure it copies the following: 

```typescript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx,mdx}',
    './components/**/*.{js,ts,jsx,tsx,mdx}',
    './app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {},
    },
  plugins: [], 
}
```

refresh your localhost to see a plain white background.

Now let's test Tailwind CSS. Go back to page.tsx and add a classname to this div: 

```typescript
  return (
   <div className="text-purple-500 text-2xl"> Welcome to My Airbnb Clone!!!</div>
  )
  ```

  Refresh your localhost and notice the color and font has changed.

  ![img](https://i.imgur.com/23bk21n.png)

The last step in setting the environment is to go back into your global.css folder and copy the following: 

```typescript 
html,
body,
:root {
  height: 100%
}
```
You will notice no changes upon refreshing of your localhost because this is just the setup for all the elements we are going to input later.  

Great job you have now successfully created the environment. Or the Skeleton if you will. 

## Creating The Navigation Bar

Now let's add our navigation bar. 

Go to your >app folder into layout.tsx 

Let's collapse the {children} in the body element below and add a Navbar tag. 

<img src=https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzcyMzRjMTllMDYyOGIzMTNiOTE3MzU2YTNjNmEzY2RmOTA2YTQ4YSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/FHmuQubMuPHdQte6o0/giphy.gif>

```typescript 
  return (
    <html lang="en">
      <body className={font.className}>
        <Navbar />
        {children}
      </body>
    </html>
  )
}
```

Refresh your local host and you'll see an error because Navbar is not defined. 

![navbar not defined](https://i.imgur.com/t4LXqlz.png)

## Navbar: Components Folder

Alright, let's get started by going into the "app" folder and creating a new folder called "components" 

*I must mention, though, that it's not mandatory to write your components inside this specific folder. You have the freedom to organize them as you please. However, for the sake of this tutorial and to satisfy my brain's craving for organization, let's go ahead and open a components folder.* 

Just remember, you can write your components wherever you find it most convenient!

Inside your components folder, create a new folder called "navbar." 

Then in that folder, create a new file called "navbar.tsx."  

This is so you can seperate your components nicely.

For this next step, make sure you have React Snippets extension installed in VS Code (I know I didn't. Thanks Babe <3)

Name your component Navbar and add a div to identify the navbar when you refresh your localhost. 

```typescript
const Navbar  = () => {
    return ( 
        <div>
            Place Navbar Here! 
        </div>
     );
}

export default Navbar;
```

It should look like a pile of caca so let's fix it. 

![img](https://i.imgur.com/Efz5FDf.png)

Add a className to your div in your Navbar component. 

The first div is going to have a className of 


```typescript
const Navbar  = () => {
    return ( 
        <div className="fixed w-full bg-white z-10 shadow-sm">
            Place Navbar Here! 
        </div>
     );
}

export default Navbar;
```
![img](https://i.imgur.com/6aEtu9b.png
)
We have our little navbar here with a small shadow, and our body has currently disappeared. That's because we have put a fixed position on this navbar, but we're going to fix that later with some padding.

Inside, create another div which is going to have 
the following styles: 

```typescript
const Navbar  = () => {
    return ( 
        <div className="fixed w-full bg-white z-10 shadow-sm">
          <div
            className="
             py-4
             border-b-[1px]
             "
            >
    
          </div>
        </div>
     );
}

export default Navbar;
```
![navbar](https://i.imgur.com/O8pyzFm.png)

That is going to enforce how you see this navbar. You can see how we can clearly distinguish between the body and the navbar here at the top.

## Navbar: Container

Now inside of that div, we're going to create another component. For now, all I want to do is write 'Container', 

```typescript
const Navbar  = () => {
    return ( 
        <div className="fixed w-full bg-white z-10 shadow-sm">
          <div
            className="
             py-4
             border-b-[1px]
             "
            >
             <Container>
                
             </Container>
    
          </div>
        </div>
     );
}

export default Navbar;
```

and you can just save. You'll get an error because 'Container' does not exist yet. 

Let's go ahead and go into our components folder and create a new file called 'Container.tsx'. 

Your structure should look something like this:

![structure](https://i.imgur.com/29jT3ZP.png)

'Container' is going to be reused across the app, while all of the components we write in 'Navbar' are only going to be for 'Navbar'.

Let's go into 'Container.tsx' and do the same thing: 

```typescript
const Container = () => {
    return (
        <div>Container</div>
      );
}
 
export default Container;
```

![container](https://i.imgur.com/yBpnFgY.png)

let's write an interface above the constant in Container.tsx using React. 

```typescript
interface ContainerProps {
    children: React.ReactNode;
}
```
Interface container props is going to be children, which is a type of react.react node. 

And now, we can assign these props or properties to this element. 

```typescript
interface ContainerProps {
    children: React.ReactNode;
}
```
So, react functional component container props, and you can just extract the children from the props. 
And then, you can replace the container with children. 

```typescript
const Container: React.FC<ContainerProps> = ({
    children
}) => {
    return (
        <div>{children}</div>
      );
}
 
export default Container;
```



Refresh your localhost and we no longer see our text, but if you go back into navbar.tsx and write anything in your container, you can literally write anything and save. 

![img](https://i.imgur.com/vzpZvdM.png)

You can see that it is passed as our children to the container right here. Great!

Before we move on, we want to mark this component as a client component. This is something we have to do when we work with the app folder because every component and page we create inside the app folder is a server component by default. And there can be hydration problems if you mix and match imports with client and server components.

We are going to use server components to fetch data directly from the database, but container for now is going to be a styling component. 

So let's just write use client at the top because we are going to import this container in other client components. So, it's important that this is also a client component.

```typescript
'use client';

interface ContainerProps {
    children: React.ReactNode;
}
```

 Great!

Now collapse the children in the folder Container.tsx to write the following classnames in the div.

```typescript
const Container: React.FC<ContainerProps> = ({
    children
}) => {
    return (
        <div
        className="
         max-w-[2520px]
         mx-auto
         xl:px-20
         md:px-10
         sm:px-2
         px-4
        "
      > 
        {children}
        </div>
      );
}
 
export default Container;
```
![img](https://i.imgur.com/6CVdyOd.png)

There, and you can see how now we have this bit of spacing that we have created. Great! 

Now go back into your navbar component and in your container add a div and write some other elements. 

```typescript
const Navbar  = () => {
    return ( 
        <div className="fixed w-full bg-white z-10 shadow-sm">
          <div
            className="
             py-4
             border-b-[1px]
             "
            >
             <Container>
               <div
                className="
                 flex
                 flex-row
                 items-center
                 justify-between
                 gap-3
                 mc:gap-0
                "
               >
        
               </div>
             </Container>
    
          </div>
        </div>
     );
}

export default Navbar;
```

Next, let's add a logo component like simply adding under the div above.

```
<Logo />
```

Refresh your localhost and you'll see an error because we need to define this component. 

Create a new file inside components inside the navbar folder as we're only changing the style of the navigation bar and label it logo.tsx. 

Your folders should be organized like this now.  
![img](https://i.imgur.com/6NMO77R.png)

And you can already guess that this component is also going to be needed to be a client component. 

So, at the top, we're going to write use client like this. 

And the next thing we're going to do is import image from next/image.

```typescript
'use client';

import Image from "next/image";
import { useRouter } from "next/navigation";
```

And we are also going to import our router, but be careful how I'm going to do this. So, import useRouter. 

And you might be thinking, "Well, I already know this. It's from next/router." 

But in the next 13, we're using the new package, so write import useRouter from next/navigation.

```typescript
const Logo = () => {
    const router = useRouter();

    return (
        <Image
         alt="Logo"
         className="hidden md:block cursor-pointer"
         height="100"
         width="100"
         src="/images/logo.png"
        />
    )
    }
export default Logo; 
```
Now, let's write our components. So, `const Logo` is going to use the router, so just write useRouter like this. And it's going to return an image element.

Now, let's add some attributes to this image element. The alt is going to be "logo." The class name is going to be "hidden" on small or mobile devices. On MD, it's going to turn into a block device. And cursor is going to be "pointer."

Great! Now, let's add the height, which is 100, and the width, which is also 100. And the last thing we have left is the source. The source is going to be /images/logo.png.

To prep, download [this image ](https://raw.githubusercontent.com/AntonioErdeljac/next13-airbnb-clone/master/public/images/logo.png)into your public folder and name it logo.png. 

Save and refresh your local host to be greeted with your first visual. 

![img](https://i.imgur.com/1CJYC3a.png)

## Navbar: Search Filters 

Before we continue, let's doublecheck that you have everything in the right folder like below. 

<img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExNDdlNTA1ZWQyYWZjN2MzNTBhZDY3NzEwOTI2MWRlM2JlZGU5NDQzZiZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/iMjRrMZfPQZs10oImJ/giphy.gif">

Now lets do a few things we've done already: 

- add a new file under navbar in your components folder to add Search filters and label it `Search.tsx`

- add your `const` and label it Search and let's add a `<div></div>` for now. 

- we are also making this file a client component.

```typescript
'use client'; 

const Search = () => {
    return (
        <div>
            
        </div>
      );
}
 
export default Search;
```

- next type in `<Search />` under `<Logo />` in your `navbar.tsx` file and import it like so: 

<img src=
https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExZWFiMmRmOTEzOGI5MjRkZGQwYmI0NmYwNTM2ZTVkN2E5ZGY1MzI4NiZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/DxB7OUV9P92OXsnZLc/giphy.gif>

Now our Search Filter component is all set up. 

Before we move on, let's install one additional package. 

Open your terminal, clear, and run `npm install react-icons`

Back in your Search.tsx folder we're back at that `<div>` we made earlier. 

## Four... Hundred ....Thousand `<div>`s

Add the following classNames 

```typescript
'use client';

const Search = () => {
    return (
        <div
         className="
          border-[1px]
          w-full
          md:w-auto
          py-2
          rounded-full
          shadow-sm
          hover:shadow-md
          transition
          cursor-pointer
          "
        >
            
        </div>
```

Below that `<div>` let's add some more elements.

>include {BiSearch} instruction here

```typescript
'use client';

import { BiSearch } from 'react-icons/bi';

const Search = () => {
    return (
        <div
         className="
          border-[1px]
          w-full
          md:w-auto
          py-2
          rounded-full
          shadow-sm
          hover:shadow-md
          transition
          cursor-pointer
          "
        >
         <div
          className="
           flex
           flex-row
           items-center
           justify-between
          "
         >
            <div
             className="
             text-sm
             font-semibold
             px-6
             "
            >
                Anywhere 
            </div>
            <div
             className="
             hidden
             sm:block
             text-sm
             font-semibold
             px-6
             border-x-[1px]
             flex-1
             text-center
             "
            >
               Any Week
            </div>
            <div
              className="
               text-sm
               pl-6
               pr-2
               text-gray-600
               flex
               flex-row
               items-center
               gap-3
               "
            >
            <div className="hidden sm:block"> Add Guests </div>
            <div
             className="
              p-2
              bg-rose-500
              rounded-full
              text-white
              "
            >
                <BiSearch size={18} />

              </div>
            </div>
          </div>
        </div>
      );
}
 
export default Search;
```

## NAV BAR Last Element: USER MENU

This is going to be our button when we click its going to open the rent model. There is no functioniality for that of course but we will add that later. with `onClick={(=>{})}`

```typescript
'use client';

import {AiOutlineMenu} from 'react-icons/ai';
import Avatar from '../Avatar';

const UserMenu = () => {
    return (
        <div className="relative">
            <div className= "flex flex-row items-center gap-3">
                <div
                 onClick={()=>{}}
                 className="
                  hidden
                  md:block
                  text-sm
                  font-semibold
                  py-3
                  px-4
                  rounded-full
                  hover: bg-neutral-100
                  transition
                  cursor-pointer
                  "
                >
                    Airbnb your home

                </div>
                <div
                 onClick={()=>{}}
                 className="
                  p-4
                  md:py-1
                  md:px-2
                  border-[1px]
                  border-neutral-200
                  flex
                  flex-row
                  items-center
                  gap-3
                  rounded-full
                  cursor-pointer
                  hover:shadow-md
                  transition
                  "
                >
                    <AiOutlineMenu />
                    <div className="hidden md:block">
                        <Avatar />
                    </div>

                </div>

            </div>
        </div>
      );
}
 
export default UserMenu;
```

Let's make the little button into a hamburger using `import {AiOutlineMenu} from 'react-icons/ai'`

and add `<AiOutlineMenu />` under the last `<div>` above. 


## Creating Avatar Component

In components, not under navbar, we're going to create the avatar component because we're going to be using these across the interface. 

```typescript
`use client`;

import Image from "next/image";

const Avatar = () => {
    return ( 
        <Image
          className="rounded-full"
          height="30"
          width="30"
          alt="Avatar"
          src="/images/placeholder.jpeg"
        />
     );
}
 
export default Avatar;
```


























