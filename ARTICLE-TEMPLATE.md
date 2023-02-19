## React Form and Validation with Formik and Yup 

Creating forms in React can be very tedious and time consuming especially when you have to validate the form.

This is because you have to create a state for each input field, create a function to handle the change event and then validate the form, but this can be much tougher as the number of input fields increases.

In this article, we will learn how to create a form in React and validate it using Formik and Yup.

## Prerequisites

To better follow this article, you should have
- a basic understanding of React and JavaScript
- a web browser (preferably Chrome)
- Node.js installed on your computer
- React.js installed on your computer
- A text editor (preferably VS Code)
- A cup of water or coffee

## What is formik and yup?

Formik is an open source library for creating forms in React and React Native. It helps you with the three most important things when building forms with React: managing your form state, validating your form, and handling form submission.

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

You can check out more about Formik [here](https://formik.org/)

## What is Yup?

Yup is a schema builder for runtime value parsing and validation. Yup schema are extremely expressive and allow modeling complex, interdependent validations, or value transformations.

In React forms, Yup is used to validate the form.

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

You can check out more on Yup [here](https://www.npmjs.com/package/yup)

In the next section, we will create a user data form with React and Yup for validating the user data in the form.

## Creating a React app 

First, let's create a react application named "react-formik-yup" using the create-react-app command as seen below 

```bash
npx create-react-app react-formik-yup
```
### Installing Formik and Yup

To install Formik and Yup, run the following command in your terminal

```bash
npm install formik yup
```

### Starting application locally 

Next, navigate into your react app and start your development server as shown below

```bash
cd react-formik-yup
npm start
```

## Building the React form 

In this section, we will build a form that will collect user data such as name, email, password and confirm password. 
Initially, we will create a form component that will contain the form fields and then we will create a validation schema for the form using Yup.

### Creating a form component

Navigate to your src folder and create a new folder named "components" and then create a new file named "Form.js" inside the components folder. In the Form.js file, add the following code:

```js
import { Formik } from 'formik';

const App = () => {
  return (
    <div className="App">
      <h1>React Form and Validation with Formik and Yup</h1>
      <Formik
        initialValues={{ name: '', email: '', password: '', confirmPassword: '' }}
        onSubmit={(values) => {
          console.log(values);
        }}
      >
        {({ values, handleChange, handleSubmit }) => (
          <form onSubmit={handleSubmit}>
            <label htmlFor="name">Name</label>
            <input
              type="text"
              name="name"
              id="name"
              value={values.name}
              onChange={handleChange}
            />
            <label htmlFor="email">Email</label>
            <input
              type="email"
              name="email"
              id="email"
              value={values.email}
              onChange={handleChange}
            />
            <label htmlFor="password">Password</label>
            <input
              type="password"
              name="password"
              id="password"
              value={values.password}
              onChange={handleChange}
            />
            <label htmlFor="confirmPassword">Confirm Password</label>
            <input
              type="password"
              name="confirmPassword"
              id="confirmPassword"
              value={values.confirmPassword}
              onChange={handleChange}
            />
            <button type="submit">Submit</button>
          </form>
        )}
      </Formik>
    </div>
  );
};
```

In the code above, we imported the Formik component from the formik library and then we created a form component that contains the form fields, for name, email, password and confirm password. We then added a submit button.

In the next section, we will create a validation schema for the form using Yup. 

### Creating a validation schema for the form

To create a validation schema for the form, navigate to your src folder and create a new file named "validationSchema.js" and add the following code:

```js
import * as Yup from 'yup';

const validationSchema = Yup.object().shape({
  name: Yup.string().required('Name is required'),
  email: Yup.string().email('Email is invalid').required('Email is required'),
  password: Yup.string()
    .min(6, 'Password must be at least 6 characters')
    .required('Password is required'),
  confirmPassword: Yup.string()
    .oneOf([Yup.ref('password'), null], 'Passwords must match')
    .required('Confirm Password is required'),
});

export default validationSchema;
```

In the code above, we imported the Yup object from the yup library and then we created a validation schema for the form. We then exported the validation schema.

You can see the validation schema for the form in the code above. We used Yup.string() to validate the name, email and password fields. We also used Yup.string().required() to validate the confirm password field. You can learn more on Yup methods [here](https://www.npmjs.com/package/yup)

## Adding Yup Validation to the Form

In this section, we will add the Yup validation schema to the form component. To do this, visit the Form.js file and add the following code:

```js
import { Formik } from 'formik';
import validationSchema from './validationSchema';

const App = () => {
  return (
    <div className="App">
      <h1>React Form and Validation with Formik and Yup</h1>
      <Formik
        initialValues={{ name: '', email: '', password: '', confirmPassword: '' }}
        validationSchema={validationSchema}
        onSubmit={(values) => {
          console.log(values);
        }}
      >
        {({ values, handleChange, handleSubmit }) => (
          <form onSubmit={handleSubmit}>
            <label htmlFor="name">Name</label>
            <input
              type="text"
              name="name"
              id="name"
              value={values.name}
              onChange={handleChange}
            />
            <label htmlFor="email">Email</label>
            <input
              type="email"
              name="email"
              id="email"
              value={values.email}
              onChange={handleChange}
            />
            <label htmlFor="password">Password</label>
            <input
              type="password"
              name="password"
              id="password"
              value={values.password}
              onChange={handleChange}
            />
            <label htmlFor="confirmPassword">Confirm Password</label>
            <input
              type="password"
              name="confirmPassword"
              id="confirmPassword"
              value={values.confirmPassword}
              onChange={handleChange}
            />
            <button type="submit">Submit</button>
          </form>
        )}
      </Formik>
    </div>
  );
};
```

In the code above, we imported the validationSchema from the validationSchema.js file and then we added the validationSchema to the Formik component. Our form is now ready to validate the user data. 

## Conclusion

In this tutorial, we have learned how to create a React form and validate the user data in the form using Formik and Yup. We have also learned how to create a validation schema for the form using Yup.

You can check out the full code for this tutorial [here](/link to github)

## Resources and References

You can check out some of the resources listed below to learn more about Formik and Yup

- [Formik](https://formik.org/)
- [Yup](https://www.npmjs.com/package/yup)
- [React Formik Tutorial](https://www.youtube.com/watch?v=oiNtnehlaTo)
- [React Form Validation Tutorial](https://www.youtube.com/watch?v=9Qk-1IXRfew)