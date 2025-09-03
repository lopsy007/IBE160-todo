# 6. Epic Details

### Epic 1: Foundation & Core Task Management

This epic focuses on setting up the project's infrastructure and implementing the basic features of a to-do application.

**Story 1.1: Project Setup**
As a developer,
I want to set up the monorepo with the mobile app project, backend services, and CI/CD pipeline,
so that we have a solid foundation for development.

*Acceptance Criteria:*
1.  A monorepo is created in Git.
2.  A basic "Hello World" React Native/Flutter app is created.
3.  A serverless backend project is set up.
4.  A CI/CD pipeline is configured to run tests on every commit.

**Story 1.2: User Authentication**
As a student,
I want to be able to sign up and log in to the app,
so that my tasks are saved securely.

*Acceptance Criteria:*
1.  Users can sign up with an email and password.
2.  Users can log in with their credentials.
3.  User sessions are managed securely.

**Story 1.3: Basic Task Management**
As a student,
I want to be able to create, view, edit, and delete tasks,
so that I can manage my to-do list.

*Acceptance Criteria:*
1.  I can add a new task with a title.
2.  I can see a list of my tasks.
3.  I can edit the title of a task.
4.  I can delete a task.
5.  Tasks are persisted in the database.

### Epic 2: The Motivational Loop

This epic focuses on implementing the core features that make the app motivating and engaging.

**Story 2.1: Complete a Task**
As a student,
I want to mark a task as complete and feel a sense of accomplishment,
so that I am motivated to complete more tasks.

*Acceptance Criteria:*
1.  I can mark a task as complete from the task list.
2.  When a task is marked complete, a celebratory animation is shown.
3.  Completed tasks are moved to a separate "Completed" view.

**Story 2.2: Overdue Tasks**
As a student,
I want the app to be encouraging when I miss a deadline,
so that I don't feel demotivated.

*Acceptance Criteria:*
1.  Overdue tasks are clearly marked in the UI.
2.  The language used for overdue tasks is encouraging (e.g., "Still got this?").
3.  There are no punitive elements for overdue tasks.
