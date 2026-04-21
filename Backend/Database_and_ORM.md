# Database and ORM Concepts

## Mongoose & MongoDB (Bank Ledger Example)
1. `mongoose.connect`: Returns a promise. Can be handled by `async/await` or `.then() / .catch()`.
2. Schema Design: `required: true` or `required: [true, "Email is required"]` for custom validation messages.
3. Pre-save hooks for password hashing:
    ```javascript
    // whenever you 'save' user data, this function will run first
    userSchema.pre("save", async function(next){
        if(!this.isModified("password")) return next();

        this.password = await bcrypt.hash(this.password, 10);
        next();
    });
    ```
4. Custom Schema Methods (Compare Password):
    ```javascript
    // compare password - saved/old password and new password
    userSchema.methods.comparePassword = async function(password){
        return await bcrypt.compare(password, this.password);
    };
    ```
5. Multiline comments: Use so when a function name format is hovered over, it can show the required data/documentation for another developer.

## Database Errors
- "Duplicate Key" Error:
  - If a schema is created and DB is connected to it, changing a property name after that can throw a "Duplicate Key" error.
  - The DB will still try to get data from the old property name (especially because of old unique indexes).
  - You often have to drop the collection/index and create it again.
