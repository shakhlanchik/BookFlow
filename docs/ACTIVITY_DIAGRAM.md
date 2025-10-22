# BookFlow - Activity Diagrams

## Overview
Activity diagrams are used to model the dynamic aspects of the system. They provide a visual representation of the flow of actions and decisions, effectively illustrating the workflow from a starting point to an end point. This section details the primary workflow a user follows when engaging in a reading session.

## Reading Session Workflow

### Description
This diagram models the core user journey within the BookFlow application. It begins when a user selects a book from their library and proceeds through the interactive reading process, which includes a loop for customization. The workflow concludes when the user closes the book and returns to the library. This entire lifecycle represents the primary value proposition of the application.

### Diagram

![Reading Session Workflow](/docs/diagrams/activity_diagram.png)

### Workflow Steps Explained:

1.  **Start and Selection**: The process begins in the Library Screen, where the user can see their collection of books. The user initiates the workflow by tapping on a specific book they wish to read.

2.  **Loading and Display**: The system takes over, loading the book's file from local storage and retrieving the user's last saved reading progress (e.g., the last page number). It then transitions to the Reader View, displaying the book's content at the correct position.

3.  **Interactive Reading Loop**: The user now enters the main interactive cycle.
    *   The user reads the content and turns pages using swipe gestures or taps.
    *   With each page turn, the system automatically saves the new progress to the local SQLite database in the background. This ensures the user never loses their spot.
    *   This loop continues as long as the user is actively reading.

4.  **User Decision Point**: While in the reading loop, the user can choose to perform another action.
    *   **Path A: Continue Reading**: The default action is to simply continue turning pages, remaining in the loop.
    *   **Path B: Customize View**: The user can decide to open the settings menu.

5.  **Customization Sub-Flow**:
    *   If the user opens the settings, a settings overlay or menu is displayed.
    *   The user can adjust parameters like font size or background color.
    *   The Reader View updates instantly to provide a live preview of the changes.
    *   Once the user closes the settings menu, they are returned to the main interactive reading loop.

6.  **End and Return**:
    *   When the user is finished reading, they tap a "Back" or "Close" button.
    *   The system performs one final save of their progress to ensure the very last position is recorded.
    *   The application navigates the user back to the Library Screen, concluding the workflow.
