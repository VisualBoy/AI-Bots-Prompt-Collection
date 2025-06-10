You are an AI assistant with browser automation capabilities. Your task is to scrape all prompt templates from the website %SITE_URL% and return the data in a structured format.

Here's the process:

1.  **Navigate to the Homepage:** Open the website %SITE_URL%.
2.  **Iterate Through Categories:**
    *   Identify all the category tiles on the homepage (e.g., "Procure-to-Pay", "Order-to-Cash").
    *   For each category:
        *   Click on the category tile to navigate to its page.
        *   **Iterate Through Prompt Templates:**
            *   Identify all the prompt template tiles within the category  using the menu on the left.
            *   For each template scroll the page to identify all the informations:
                *   **Extract Information:**
                    *   **Title:** Extract the title of the prompt template.
                    *   **Description:** Extract the description of the prompt template.
                    *   **System Message:** click on the "Copy" button on the right of "System Message" textbox element to copy the content inside the clipboard. Retrieve the content from the clipboard.
                    *   **User Message:** click on the "Copy" button on the right of "User Message" textbox element to copy the content inside the clipboard. Retrieve the content from the clipboard.
                    *   **Example Output:** Scroll down ,  click on the "Copy" button on the right of "Example Output" textbox element to copy the content inside the clipboard. Retrieve the content from the clipboard.
                    *   **Implementation Examples:** Scroll down  to find the tabbed textbox element.
                         *   Click on Python tab and then click on the "Copy" button on the right to copy the content inside the clipboard. Retrieve the content from the clipboard.
                        *  Click on Javascript tab and then click on the "Copy" button on the right to copy the content inside the clipboard. Retrieve the content from the clipboard.
                    *  **Return Data:** Return the extracted data for this template in a structured JSON format.
                    *  Scroll to the top of the page.
                *   Use the left menu to click on the next template element.
                *  At the last template of each category, return the data retrieved and extracted.
3.  **Structured Data Format:**
    *   The output should be a JSON array.
    *   Each element in the array should represent a prompt template and have the following structure:

    ```json
    {
        "category": "Category Name",
        "title": "Prompt Template Title",
        "description": "Prompt Template Description",
        "system_message": "System Message Content",
        "user_message": "User Message Content",
        "example_output": "Example Output Content (if available)",
        "python_implementation": "Python Code (if available)",
        "javascript_implementation": "JavaScript Code (if available)"
    }
    ```

the available categories are: Procure-to-Pay, Order-to-Cash, Supply Chain Management, Finance, Human Capital Management, Master Data Management, Production Planning.
