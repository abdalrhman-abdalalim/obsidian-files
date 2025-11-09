# How `isActive` is Determined in React Router's NavLink

The `isActive` parameter is determined by React Router's `NavLink` component based on the current URL and the link's `to` prop. Here's how it works:

## Basic Matching

By default, `NavLink` checks if the current URL **starts with** the `to` path:

// Current URL: /dashboard/premium/tracks
// NavLink to: /dashboard/premium

`isActive = true // Because /dashboard/premium/tracks starts with /dashboard/premium`

## The `end` Prop

When you use `end={true}`, it changes to **exact matching**:

// Current URL: /dashboard/premium/tracks
// NavLink to: /dashboard/premium with end={true}

`isActive = false // Because it requires exact match`


// Current URL: /dashboard/premium
// NavLink to: /dashboard/premium with end={true}

`isActive = true // Exact match`

## How React Router Determines isActive

1. **Without `end` prop**: URL starts with the `to` path
    
    - `to="/products"` matches `/products`, `/products/123`, `/products/new`
        
2. **With `end={true}`**: URL exactly matches the `to` path
    
    - `to="/products"` with `end={true}` only matches `/products`
        

## Visual Examples

|Current URL|NavLink `to`|`end`|`isActive`|
|---|---|---|---|
|`/dashboard/premium`|`/dashboard/premium`|`false`|`true`|
|`/dashboard/premium`|`/dashboard/premium`|`true`|`true`|
|`/dashboard/premium/tracks`|`/dashboard/premium`|`false`|`true`|
|`/dashboard/premium/tracks`|`/dashboard/premium`|`true`|`false`|
|`/dashboard/premium/courses`|`/dashboard/premium`|`false`|`true`|
|`/dashboard/premium/courses`|`/dashboard/premium`|`true`|`false`|

## Your Specific Case

In your sidebar, you have:

- Overview: `to="/dashboard/premium"` with `end={true}`
    
- Tracks: `to="/dashboard/premium/tracks"` (no `end` prop)
    
- Courses: `to="/dashboard/premium/courses"` (no `end` prop)
    

This means:

- Overview is only active when URL is exactly `/dashboard/premium`
    
- Tracks is active when URL starts with `/dashboard/premium/tracks`
    
- Courses is active when URL starts with `/dashboard/premium/courses`
    

## Advanced: Custom Matching

You can also provide a custom function for more complex matching:

tsx

<NavLink
  to={to}
  className={({ isActive, isPending }) => 
    isActive ? "active" : isPending ? "pending" : ""
  }
  // Custom matching function
  isActive={(match, location) => {
    if (!match) return false;
    // Add custom logic here
    return match.url.indexOf("/special") !== -1;
  }}
>
  {label}
</NavLink>

## Key Points

1. **Default behavior**: Partial matching (URL starts with `to` path)
    
2. **`end={true}`**: Changes to exact matching
    
3. **Order matters**: The first matching `NavLink` gets the active state
    
4. **Multiple active links**: Possible if you have nested routes without `end` prop