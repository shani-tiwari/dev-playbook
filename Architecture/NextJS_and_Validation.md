# NextJS and Validation

## Mongoose in NextJS

- **Mongoose and Database Modeling & TypeScript Integration:** Always define an `interface` for your data structures. This ensures type safety and clarity when interacting with the database.     

- **Document Handling:** Use the `Document` type from Mongoose when defining your schemas to properly type your database models in Next.js.

- **Model Exporting:** Because Next.js often operates in serverless or edge environments, check if a model already exists before defining it again. This prevents re-initialization errors by using a pattern like `mongoose.models.User || mongoose.model(...)`.     

## Connect to DB (Serverless Ecosystem)

- **Understanding the Lifecycle:** Unlike standard backend applications that run continuously, Next.js operates on an on-demand basis. The application code executes only when a user makes a request, meaning the database is not kept connected at all times.            

- **Preventing Database Choking:** Because Next.js functions run per-request, you must check for an existing database connection before attempting to create a new one.          

- **Connection Strategy:** Always implement a verification step in your connection logic. If a connection is already active, reuse it. If not, only then proceed to establish a new one.    

- **Project Structure:** It is recommended to keep your database connection utility inside a `lib` folder. This is a best practice, especially if you plan to integrate tools like shadcn/ui later, which also utilize this directory.            

- **Environment Variables:** Use a `.env` file to securely store your database URI. Next.js handles these environment variables automatically, so you can access them using `process.env`.        

- **TypeScript:** When defining your connection object, use TypeScript types (like `isConnected`) to maintain clarity and avoid runtime errors. 

## Zod Validation

- **Zod Validation Best Practices (Schema-First Validation):** Use Zod to validate incoming data before it touches your database. This acts as a primary gatekeeper for your application.   

- **Chaining Methods:** Such as `z.string().min(2).max(20)`, to perform multiple checks on a single field. 

- **Custom Error Messages:** Always provide helpful, user-facing error messages inside your Zod schema configurations. This improves the user experience when validation fails.            

- **Advanced Validation:** For complex requirements, like specific email formats or strict character constraints, use Regex alongside Zod to ensure precise data matching.   

## Tips           

- Keep your validation schemas in a dedicated folder (like `src/schemas`) to maintain a clean project structure and make your code easier to maintain.  

- Maintain Consistency: While Mongoose provides database-level validation, Zod provides application-level validation. Using both together creates a more robust and secure application.         

- Case Sensitivity: Remember that Mongoose types (like `String`) and TypeScript primitive types (like `string`) are different. Misusing these can lead to subtle bugs in your schema definitions.      

- Debounce: When checking field uniqueness and want to implement debouncing with a server API request, send the username value by saving it in another variable with a delay, rather than sending the original `useState` form value directly on every keystroke.
