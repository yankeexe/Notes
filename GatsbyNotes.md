## Notes for    

**General Notes**
- All of the pages in Gatsby are basically React components. 
- Every time you update `gatsby-config.js` you have to restart the development server.

### Linking between pages with Gatsby

1. **Using Anchor Tag**
We can directly use the anchor tag `<a>` to add a hyperlink to other pages on the site. 
Example: 
```html
     <p>
        Need a developer?<a href="/contact">Contact Me</a>
      </p>
```
But the problem with this one is, it does full page refresh reloading all the contents. If we are linking outside urls then using anchor tag is fine.  Make sure to put `http or https` in url else it will open in localhost:8000/www.github.com

2. **Using Gatsby Link**

   Link is a React component. When we use Link for linking pages, there is a lot optimizations behind the scene like preload page contents.

   Since Link is a React component we pass a prop called 'to', in order to specify the url we want to link. 

   Example: 

   ```html
   <p>
     Need Developer? <Link to='/contact'> Hire 		Me </Link>
   </p>
   ```

### Creating Gatsby Page Layouts

`props.children` in React is all the elements that is passed inside of the React Component. Suppose we have a `<Layout>` Component and it holds some HTML elements. 

```jsx
// index.js
<Layout>
	<h1>Hello there</h1> <!-- props.children -->
  <p>Welcome to my page</p> <!-- props.children-->
</Layout>
```

```jsx
const Layout = props => {
  return(
  	<div>
    	{props.children}
    </div>
  )
}
```

### Installing Plugins in Gatsby

Install the plugin using npm or yarn. Create `gatsby-config.js` file on the root directory. Inside that file we have to export the modules.

**Example:** 

```js
module.exports = {
  plugins: [`gatsby-plugin-sass`]
}
```

### Styling Gatsby Projects with CSS Modules

To create a module for css file, rename the css or scss file to `filename.module.css` 

Write the class names and the styles we want to apply to that class. 

In out JS file, we need to import the module now. Suppose a css module called, `header.module.scss` with a class `link`needs to be imported on `header.js` file. 

```js
import headerStyles from './header.module.scss'
// The import name can be any name that we like, in here it is headerStyles.
<div className="headerStyles.link">Hello there </div>
```

**Active Class in CSS**

Whenever we select a tab, we need to highlight it showing that we are on that tab. To do that gatsby provides us with the `activeClassName` attribute. 

Example: 

```html
<!-- HTML -->
<Link className={headerStyles.link} activeClassName = {headerStyles.activeLink}> Blog </Link>
<Link className={headerStyles.link} activeClassName={headerStyles.activeLink}>About us</Link>
```

```css
// CSS
.active-link {
  color: green; 
  font-weight: bold;
}
```

### Gatsby Data with GraphQL

To enter in browser IDE to explore GraphQL you need to have your local server running. Suppose the url is localhost:8000 then we can enter **GraphiQL** playground using `localhost:8000/___graphql` i.e. triple underscore and graphql. 

There are three main things that we can do with graphql: 

- query 
- mutations 
- subscription

To use graphql on our app we need to import {graphql, useStaticQuery} modules from the 'graphql' package. 

`import {graphql, useStaticQuery} from 'graphql'`

To perform querying of data we need to use  the useStaticQuery function with tagged template literal.  In the example below: the graphql with backtics is the tagged template literal. Then inside of the template literal we can use the graphql query syntax that we used in the GraphiQL beginning with the `query` keyword.

**Example:**

```js
const data = useStaticQuery(graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`)
```

To fetch these data, we need to have stored the data on the `gatsby-config.js` file. 

```js
// gatsby-config.js 
module.exports = {
  siteMetadata: {
    title: "Yankeexe Site",
    author: "Yankee Maharjan",
  }
}
```

### Topic 

Cross platform environment variable to switch from GraphiQL playground to a newer GraphQL IDE playground. 

Steps: 

- One the root of the project directory create: `.env.development` file. 
- Inside that file `GATSBY_GRAPHQL_IDE=playground`
- To use this new playground on dev server we use `env-cmd` npm package (globally in my case) `npm i -g env-cmd`
- Use this package to overwrite our default `develop` command on the `package.json` file. 
  `"develop": "env-cmd .env.development gatsby develop"`

### Generating Slugs for Posts

