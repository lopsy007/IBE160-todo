# Testing Strategy

### Testing Pyramid

A standard testing pyramid will be followed to ensure a healthy and maintainable test suite.

```
      /\
     /  \   E2E Tests (Cypress)
    /____\
   /      \ Integration Tests (React Testing Library + Jest)
  /________\
 /          \ Unit Tests (Jest)
/____________\ 
```

-   **Unit Tests:** Focus on individual functions and components in isolation. These will be fast and numerous.
-   **Integration Tests:** Test the interaction between components, such as a form and its submission logic.
-   **E2E Tests:** Test complete user flows from the user's perspective, running in a real browser.

```
