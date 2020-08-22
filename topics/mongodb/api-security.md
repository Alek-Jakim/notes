### Hashing Passwords with Bcrypt

The hash method can be used to hash the plain text password. The example below
hashes the password “Red12345!”.

```javascript
const password = 'Red12345!'
const hashedPassword = await bcrypt.hash(password, 8)
// The hashed password is what would be stored in the database
```

The compare method is used to compare a plain text password against a previously
hashed password. This would be useful when logging in. The user logging in provides the
plain text password for their account. The application fetches the hashed password from
the database for that user. compare is then called to confirm it’s a match.

```javascript
const isMatch = await bcrypt.compare('red12345!', hashedPassword)
console.log(isMatch)
```

[Bcrypt Documentation](https://www.npmjs.com/package/bcryptjs)

### Securely Storing Passwords

Middleware will allow you to
automatically hash a user’s password before the user is saved to the database.

Middleware allows you to register some code to run before or after a lifecycle event for
your model. As an example, you could use middleware to register some code to run just
after a user is deleted. You could also use middleware to register some code to run just
before the user is saved. This can be used to hash passwords just before saving users to
the database.

The example below calls pre with the 'save' lifecycle event. This registers a function to run just before users are saved. The function itself checks if the password has been altered. If the password has been altered, the plain text password is overwritten with a
hashed version.

```javascript
Version 1.0 80
userSchema.pre('save', async function (next) {
const user = this
if (user.isModified('password')) {
user.password = await bcrypt.hash(user.password, 8)
}
next()
})
```