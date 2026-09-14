# Prompt Engineering Concepts

## 1. Role Prompting

I assigned a clear role and domain to each expert: Database Read Expert, Database Write Expert, Content Expert, and Orchestrator.

This technique was effective because each expert produced a different type of output. The Database Read Expert generated SQL SELECT queries, the Database Write Expert generated Python code, the Content Expert answered from the resume context, and the Orchestrator created an ordered plan of expert calls.

The separation of roles made the system easier to control than using one general prompt for every task.

## 2. Few-Shot Prompting

I provided examples that showed the experts the expected output format.

Initially, the Database Write Expert generated Python inside Markdown code fences and called db.insertRows with the wrong arguments. The operation failed. I improved the prompt by adding an exact example showing that db.insertRows requires three arguments: the table name, the column list, and the values list.

After adding the example, the expert generated valid Python and successfully added React and TypeScript to the skills table. This showed that specific examples were more effective than general instructions alone.

## 3. Structured Output and Explicit Constraints

I instructed the Orchestrator to return a Python list containing exact handle_ai_chat_request calls. I also instructed the Database Read Expert to return only a SELECT query and the Database Write Expert to return only executable Python.

These constraints helped the application know how to process each response. The Orchestrator successfully produced a plan containing a Database Read Expert call followed by a Database Write Expert call.

However, the model sometimes wrapped its output in Markdown code fences even when instructed not to. I added output cleaning before parsing or executing the generated content. Therefore, structured output instructions were effective, but defensive code was still needed to handle inconsistent model formatting.سس