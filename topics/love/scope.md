### Variables and Scope

#### Global

By default, any variable you create in Lua is global unless explicitly declared as local. This means it can be accessed and modified from anywhere in your script.

```lua
name = "John"  -- This is a global variable
function greet()
    print("Hello, " .. name) -- Accessible inside the function
end
greet()  -- Output: Hello, John

--- Even if name is declared outside the function, greet() can still access it because it's global.
```

#### Local

If you use the `local` keyword, the variable is limited to the block where it's declared (function, loop, or chunk). This helps prevent accidental modifications of variables from other parts of your program.

```lua
function test()
    local x = 10  -- Local variable, only exists inside this function
    print(x)
end

test()  -- Output: 10
print(x)  -- Error! x is not defined outside the function
```

#### Variable Scope in Blocks

Lua allows you to use local variables inside control structures like if, for, and while.

```lua
if true then
    local message = "Inside if block"
    print(message)  -- Works fine
end

print(message)  -- Error! message is not accessible outside the if block
```

#### Best practices

- Use local variables whenever possible to avoid unintended global modifications.

- Use globals only for truly shared data, like game state variables (score, player, etc.).

- Avoid accidentally creating globals by always declaring variables with local inside functions.
