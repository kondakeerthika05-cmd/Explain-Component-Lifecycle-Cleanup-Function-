# Explain-Component-Lifecycle-Cleanup-Function-
Component Lifecycle in React

The component lifecycle describes the different stages a React component goes through from the time it is created until it is removed from the screen.

In functional components, lifecycle behavior is handled using useEffect().

📌 Main Lifecycle Phases
1️⃣ Mounting (Component Creation)

👉 When the component is rendered for the first time on the screen.

What happens here?

Initial render

API calls

Event listeners

Timers

Example:

useEffect(() => {
  console.log("Component Mounted");
}, []);


✔ Empty dependency array [] → runs only once

2️⃣ Updating (Component Re-render)

👉 When state or props change, the component re-renders.

What happens here?

React updates the UI

Side effects run again if dependencies change

Example:

useEffect(() => {
  console.log("Count updated:", count);
}, [count]);


✔ Runs only when count changes

3️⃣ Unmounting (Component Removal)

👉 When the component is removed from the DOM.

Examples:

Page change

Conditional rendering

Component destroyed

This is where cleanup happens.

🧹 Cleanup Function in React

A cleanup function is used to remove side effects when:

Component unmounts

Before useEffect runs again

It helps prevent:
❌ Memory leaks
❌ Duplicate event listeners
❌ Multiple timers running

📌 How Cleanup Works

Cleanup is a function returned inside useEffect().

✅ Syntax:
useEffect(() => {
  // setup code

  return () => {
    // cleanup code
  };
}, []);

🧪 Example 1: Timer Cleanup
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running...");
  }, 1000);

  return () => {
    clearInterval(timer);
    console.log("Timer cleared");
  };
}, []);


✔ Timer stops when component unmounts

🧪 Example 2: Event Listener Cleanup
useEffect(() => {
  const handleResize = () => {
    console.log("Window resized");
  };

  window.addEventListener("resize", handleResize);

  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);


✔ Prevents multiple listeners

🔁 Cleanup on Dependency Change
useEffect(() => {
  console.log("Effect running");

  return () => {
    console.log("Cleanup before next effect");
  };
}, [count]);


✔ Cleanup runs before effect re-runs when count changes
