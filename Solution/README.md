# Puzzle #71 - Dirty Models
Carl and Jeff want to know how to implement a dirty flag without modifying model classes.

YouTube Video: https://youtu.be/vS7r-PXCjHo

Blazor Puzzle Home Page: https://blazorpuzzle.com

### The Challenge

This is a .NET 9 Blazor Web App with Global Server Interactivity

Imagine that we have an existing app with 50+ models (some having 30+ properties) and 80+ pages for editing.

The boss wants you to implement a "Dirty Flag" so that when we hit the save button, we know which fields on which models have changed, and therefore what needs to be updated.

The problem is, he wants it done in 2 hours, not a week, as was your estimate.

Your idea was to expand the getters and setters of each property in each model and set a Boolean property indicating that the model properties have changed and therefore need to be updated.

Is there a shortcut to implement dirty flags without having to modify the models?

### The Solution

One great thing about web UI is that we can keep track of everything that goes on edit-wise, and keep our models clean. Imagine having to implement dirty flags in every property of every model. 

The `@oninput` event is triggered every time the value of an input field changes. 
We can use this event to set a dirty flag for each property that has changed. 
This way, we can keep track of the modified properties without having to modify the models themselves.

```html
<div class="mb-3">
    <label for="name">Name:</label>
    <input class="form-control" @bind="customer.Name"
            @oninput='(e) => SetDirtyFlag("customer.Name", e.Value)' />
</div>

<div class="mb-3">
    <label for="email">Email:</label>
    <input class="form-control" @bind="customer.Email" 
        @oninput='(e) => SetDirtyFlag("customer.Email", e.Value)' />
</div>
```

Here's the code:

```c#
// Keep a dictionary of modified properties
private Dictionary<string, object> ModifiedProperties = new();

// This is called whenever an input field value changes
void SetDirtyFlag(string propertyName, object value)
{
    // Now we have a dictionary of modified properties and their new values
    ModifiedProperties[propertyName] = value;
}
```

Now you can just inspect the dictionary in the LocationChanged event

```c#
void OnLocationChanged(object sender, LocationChangedEventArgs e)
{
    // Check a dirty flag here if the user navigates away.
    if (ModifiedProperties.Count > 0)
    {
        // Prompt the user to save changes, or do whatever you like.

        // Clear the modified properties
        ModifiedProperties.Clear();
    }
}
```

Boom!
