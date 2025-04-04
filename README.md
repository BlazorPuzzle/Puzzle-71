# Puzzle #71 - Dirty Models
Carl and Jeff want to know how to implement a dirty flag without modifying model classes.

YouTube Video: https://youtu.be/vS7r-PXCjHo

Blazor Puzzle Home Page: https://blazorpuzzle.com

## The Challenge

This is a .NET 9 Blazor Web App with Global Server Interactivity

Imagine that we have an existing app with 50+ models (some having 30+ properties) and 80+ pages for editing.

The boss wants you to implement a "Dirty Flag" so that when we hit the save button, we know which fields on which models have changed, and therefore what needs to be updated.

The problem is, he wants it done in 2 hours, not a week, as was your estimate.

Your idea was to expand the getters and setters of each property in each model and set a Boolean property indicating that the model properties have changed and therefore need to be updated.

Is there a shortcut to implement dirty flags without having to modify the models?

