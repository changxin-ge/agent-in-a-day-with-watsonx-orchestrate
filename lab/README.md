
# Workshop Lab

## Table of Contents
- [1. Environment setup](#Environment_setup)
- [2. UI Wakthrough (Optional)](#UI_walkthrough)
- [3. Create an agent](#Create_an_agent)
- [4. The Legal Contract Comparison Agent](#The_Legal_Contract_Comparison_Agent)
  - [4.1 Initial Setup](#initial_setup)
  - [4.2 Adding an OpenAPI Tool](#adding_openapi_tool)
  - [4.3 Create Agentic Workflow](#create_agentic_workflow)
  - [4.4 Update Agent Behavior](#update_agent_behavior)
  - [4.5 Test the Agent](#test_agent)
  - [4.6 Deploy the Agent (Optional)](#deploy_agent)
- [5. Summary](#summary)

## Downloadables

Ensure you download these below files and keep them handy since we will be using them as part of the lab.

1. [Master Services Agreement - ACME Corp. 462390.docx](<documents/Master Services Agreement - ACME Corp. 462390.docx>)
2. [Modification Master Services Agreement - ACME Corp. 462390.docx](<documents/Modification Master Services Agreement - ACME Corp. 462390.docx>)
3. [read-url-openapi.json](<documents/read-url-openapi.json>)

<details open id="Environment_setup">
<summary><h2>1. Environment setup</h2></summary>

1. To access the watsonx Orchestrate console, go to the [Resources list on the IBM Cloud homepage](https://cloud.ibm.com/resources).

  ![alt text](images/image1.png)

2. Expand the **AI / Machine Learning** section and select the resource that has **watsonx Orchestrate** in the Product column, as shown above. Then click **Launch watsonx Orchestrate**.

  ![alt text](images/image2.png)

This opens the watsonx Orchestrate console.

  ![alt text](images/image3.png)

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="UI_walkthrough">
<summary><h2>2. UI walkthrough (Optional)</h2></summary>

When opening the console for the first time, you may see a pop-up prompting you to create your first agent. Click **Skip for now**.

  ![alt text](images/image4.png)

The console shows that no agents have been deployed yet. If you interact with watsonx Orchestrate at this point, not much will happen because the system has no agents available to process requests.

Go ahead and chat with watsonx Orchestrate to see how it responds.

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="Create_an_agent">
<summary><h2>3. Create an agent</h2></summary>

You are now ready to build your first agent. In this section, you will create a Knowledge Base Agent that can answer user questions by retrieving information from uploaded documents.

1. In the watsonx Orchestrate console, click either **Create or Deploy** or **Create new agent**. Both options lead to the same page.

  ![alt text](images/image6.png)

2. Enter the following in the **Name** field:

   ```
   Knowledge Base Agent
   ```

3. Enter the following in the **Description** field:

   ```
   This agent responds to the user query using the available information from the knowledge base.
   ```

4. Click **Create**.

  ![Agent Creation](images/kb_agent.png)

**Knowledge** represents information stored as embeddings in a Vector Store. When the agent receives a request, it can search the connected knowledge repository to find relevant information. You can upload documents or link to an existing repository. Once again, the description field helps the agent decide whether a knowledge search is relevant.

If you add your document as a knowledge base for the agent, it will be able to perform tasks such as summarization and Q&A with the documents.

5. Click **Knowledge** on the left menu or scroll down to the Knowledge section, then click **Choose Knowledge**.

  ![Add knowledge](images/add_kb.png)

6. Select **Upload Files** and click **Next**.

  ![Upload](images/upload.png)

7. Click **Drag and drop files here or click to upload**. Upload any file as your knowledge, for example [Master Services Agreement - ACME Corp. 462390.docx](<documents/Master Services Agreement - ACME Corp. 462390.docx>), and click **Next**.

  ![File upload](images/file_uploaded.png)

8. Add the following description and click **Save**:

   ```
   This document is a Master Services Agreement between ACME and Mango Corporation.
   ```

  ![Description](images/description.png)

9. Now start asking questions. For example:

   ```
   summarize the contract document
   ```
   ![Ask Agent](images/ask_agent.png)
   ![Testing](images/testing.png)

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="The_Legal_Contract_Comparison_Agent">
<summary><h2>4. The Legal Contract Comparison Agent</h2></summary>

This section demonstrates how to build a legal contract comparison agent that analyzes original and modified contracts to identify key differences and changes.


<details open id="initial_setup">
<summary><h3>4.1 Initial Setup</h3></summary>

1. Go to the [watsonx Orchestrate homepage](https://us-south.watson-orchestrate.cloud.ibm.com/chat).

2. Click **Create agent**.

  ![Create agent](images/create_second_agent.png)

You can choose to create the agent from scratch or from a template, once you select the type you will need to provide a name and description for your agent.

Start by entering the following:

3. **Name:**

  ```
  Legal Contract Comparison Agent
  ```
4. **Description:**

  ```
  This agent is used to compare the differences between the legal contract documents provided.
  ```

In AI agent design, descriptions are not only documentation. They are used by the system to decide which agent to route a request to, so this field is important.

5. After entering the required information, click **Create**.

  ![Create](images/image8.png)

On the next screen, you can configure additional details about your agent.

* Agents can work with **Knowledge**, a **Toolset** (which includes Tools and Agents), or both, to satisfy incoming requests.
* You can also choose the **AI model**, the **agent style**, and the **voice modality**.

You can configure all of these elements here.


* The **Toolset** contains components the agent can delegate tasks to.

  * **Tools** are functions the agent can call, such as APIs or custom code, extending the agent’s capabilities beyond what the LLM knows.
  * **Agents** are other agents, either within watsonx Orchestrate or external (such as watsonx.ai agents), that can handle a request or parts of it.

> TODO Revert back to `Default` as the agent style.
6. You can select the **Large Language Model** the agent uses and the **style**. For this agent, select **llama-3-405b-instruct** and the agent style as **Default**.

![Agent Style and Model](images/nav_1.png)

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="adding_openapi_tool">
<summary><h3>4.2 Adding an OpenAPI Tool</h3></summary>

Next step is to add the required tool for this agent. To add a tool:

1. Click **Manage agents** at the top.

  ![Manage Agents](images/manage_agents.png)

2. Click **All tools** in the left panel, then click **Create tool**.

  ![All tools](images/all_tools.png)

3. Select **OpenAPI** option.

  ![Add from file or MCP server](images/nav_2.png)

4. Click **Drag and drop an OpenAPI file here or click to upload.**

  ![Drag](images/image22.png)

5. Upload the **OpenAPI tool file** downloaded in the beginning : [read-url-openapi.json](documents/read-url-openapi.json).

  ![upload](images/image23.png)

6. **Select the checkbox** next to the operation name and click **Done**.

  <img width="800" alt="image" src="images/image24.png">

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="create_agentic_workflow">
<summary><h3>4.3 Create Agentic Workflow</h3></summary>

We will create an agentic workflow and import it as a tool to be used by the agent.

![alt text](images/flow_diagram_final.png)


Let’s go ahead and create this workflow.

1. Click **Add agents** on the left, then click the **Legal Contract Comparison Agent** you created earlier.

  ![Legal Contract Comparison Agent.png](<images/Legal Contract Comparison Agent.png>)

2. Scroll down to the **Toolset** tab and click **Add Tool**.

3. Select **Agentic workflow**.

   <img width="800" alt="image" src="images/nav_3.png">

4. Click the pencil icon next to **Edit details**.

  ![alt text](images/edit_details.png)

5. Provide a **Name** and **Description** for the workflow, then click **Save**.

   * Name:

     ```
     document comparison tool
     ```
   * Description:

     ```
     This tool is used to compare between legal contract documents.
     ```

  ![Workflow name](images/workflow_name.png)

6. Click the **+** button to start adding steps.

  ![Add option](images/add.png)

7. Select **User activity**.

  ![User activity](images/user_activity.png)

8. Click **Add +**.

  ![Add option](images/add_option.png)

9. From the **Collect from user** tab, select **File upload**.

  ![File upload](images/nav_4.png)

10. Double-click **File upload**, hover over **File upload 1**, and click the pencil icon.

  ![Pencil Icon](images/nav_5.png)

11. Update the title to:

```
Upload the original Contract
```

Then click the checkmark.

  ![Update name](images/nav_6.png)

12. Click **+** below the the File upload block we just created.

  ![alt text](images/nav_7.png)

13. Click on the **Create new** tab.

  ![alt text](images/nav_8.png)

14. Select the **Text Extractor** Option.
  
  ![alt text](images/nav_9.png)

15. Double-click **Text extractor 1**, hover over it, and click the pencil icon.

  ![alt text](images/nav_10.png)

16. Update the title to:

```
Text extractor original
```

  ![Rename](images/nav_11.png)

17. Click **+** below the green User Axtivity block.

  ![alt text](images/nav_12.png)
  
18. Open the **Tools** tab and click the **+** icon next to **Fetch text content from URL**.

  ![alt text](images/nav_13.png)

19. Double click **Fetch text content from URL**, hover over it, and click the pencil icon.

20. Update the title to:

```
Fetch text content from URL original
```

  ![Rename](images/nav_14.png)

21. Click **Edit data mapping**.

  ![mapping](images/nav_15.png)

22. Hover over to the **url** row and click the **{x}** icon.

  ![Mapping](images/mapping2.png)

23. From the left, select **Text extractor original**, then select **output_file_ref**.

  ![Output file ref](images/nav_16.png)

24. Click the close button.

  ![Close](images/close2.png)

25. Click **+** below the tool block we just created.

  ![alt text](images/nav_17.png)

26. Select **User activity**.

  ![alt text](images/nav_18.png)

27. Click **Add +**.

  ![Add option](images/nav_19.png)

28. From the **Collect from user** tab, select **File upload**.

  ![File upload](images/nav_20.png)

29. Double-click **File upload**, hover over **File upload 1**, and click the pencil icon.

  ![Pencil Icon](images/nav_21.png)

30. Update the title to:

```
Upload the Modified Contract
```

Then click the checkmark.

  ![Update name](images/nav_22.png)


31. Click **+** below the the File upload block we just created.

  ![alt text](images/nav_23.png)

32. Click on the **Create new** tab.

  ![alt text](images/nav_24.png)

33. Select the **Text Extractor** Option.
  
  ![alt text](images/nav_25.png)

34. Double-click **Text extractor 1**, hover over it, and click the pencil icon.

  ![alt text](images/nav_26.png)

35. Update the title to:

```
Text extractor modified
```

  ![Rename](images/nav_27.png)


36. Click **+** below the green User Axtivity block.

  ![alt text](images/nav_28.png)
  
37. Open the **Tools** tab and click the **+** icon next to **Fetch text content from URL**.

  ![alt text](images/nav_29.png)

38. Double click **Fetch text content from URL**, hover over it, and click the pencil icon.

39. Update the title to:

```
Fetch text content from URL modified
```

  ![Rename](images/nav_30.png)

40. Click **Edit data mapping**.

  ![mapping](images/nav_31.png)

41. Hover over to the **url** row and click the **{x}** icon.

  ![Mapping](images/nav_32.png)

42. From the left, select **Text extractor modified**, then select **output_file_ref**.

  ![Output file ref](images/nav_33.png)

43. Click the close button.

  ![Close](images/nav_34.png)


44. Click **+** below the tool block we just created.

  ![alt text](images/nav_35.png)

45. Select **User activity**.

  ![alt text](images/nav_36.png)

46. Click **Add +**, Go to **Display to user** tab and select the **Message** option.

  ![Add option](images/nav_37.png)

47. Double click on the Message box and enter the below description
```
Comparing the documents, this may take a few minutes.
```
  ![Add option](images/nav_38.png)

49. Click on the **+** below the green user activity block we just created
  ![Add option](images/nav_39.png)


50. From the **Create new** tab, select **Generative prompt**.

  ![Generative Prompt](images/nav_40.png)

51. Click the pencil icon next to **Prompt Settings**.

  ![Prompt Settings](images/nav_41.png)

52. Under **Define Prompts**, click **Add**.

  ![Define Prompts](images/define_prompts.png)

53. Select **String**.

  ![string](images/strings.png)

54. Under **Name**, enter:

```
original_document_content
```

55. Click **Add**.

  ![Original Document Content](images/og_doc_content.png)

56. Add another input with the following name:

```
modified_document_content
```

  ![Modified Document Content](images/modified_doc_content.png)

57. For the **system prompt**, enter the following:

```
You are an Expert Legal Contract Comparison Agent.

You will receive two inputs:
	1.	Original Document
	2.	Modified Document

Your task: Detect and list every difference found in the Modified Document relative to the Original Document.

OUTPUT FORMAT:
Your response must start immediately with the following structure and contain only the differences:

1. (Title of the difference)
    - Section: where change occurs
    - Original Text:
    - Modified Text:
    - Nature of Change: Added / Removed / Altered

List every difference using this format.

EXAMPLES:
Eg1: 
1. Effective date updated
- Section 1 Overview
- Original Text: Effective date on **2025-11-17**
- Modified Text: Effective date on **2026-11-17**
- Nature of Change: Altered

Eg2: 
2. Reference change
- Section 1 Overview
- Original Text: Refer to section **2.5**
- Modified Text: Refer to section **2.9**
- Nature of Change: Altered

Eg3: 
3. Agreement change
- Section 1.5 Overview Details
- Original Text: Client **agrees** to abc clause
- Modified Text: Client **doesn’t agree** to abc clause
- Nature of Change: Altered

Eg4:
4. Added a paragraph in the payment clause
- Section 8 Payment Clause
- Original Text: Missing the paragraph
- Modified Text: Added **xyz...**
- Nature of Change: Added

Eg5:
5. Removed delivery clause section
- Section 19 Delivery Clause
- Original Text: **abc...**
- Modified Text: Removed the clause
- Nature of Change: Removed

STRICT RULES:
You MUST:
	•	Start your response immediately with the formatted output—no introduction, no explanation.
	•	Provide only the list of differences, nothing more.
	•	Write concisely, but with enough detail to make each change understandable.
	•	Use "..." when the surrounding text is irrelevant.
	•	Place "**" around the exact modified terms in both the original and modified texts.
	•	Identify every change—additions, removals, and alterations—even punctuation or formatting changes.
	•	If a change occurs in a table, present your result in a table format.
	•	Provide all differences—multiple changes within the same section must all be listed.

You MUST NOT:
	•	Do not repeat the same change more than once.
	•	Do not invent differences that are not present.
	•	Do not alter any quoted text from the documents.
	•	Do not skip small or “minor” differences.
	•	Do not add comments, thought process, reviews, summaries, or reasoning.
	•	Do not include anything outside the required output format.
```
58. For the **user prompt**, enter the following:

```
Here are the original and modified versions of the same document that I want you to compare.

[The Original Document]
{self.input.original_document_content}
[END of the Original Document]

[The Modified Document]
{self.input.modified_document_content}
[END of the Modified Document]
```

  ![Prompts](images/nav_42.png)

59. Click **Adjust LLM settings** and 
  - Set the max limit for **New tokens** to **2000** by sliding the scrollbar to the **rightmost**.
  - Drag the scrollbar for **the Creative Threshold** to the **leftmost** to make it **More precise**
  - Click on the model and Select the model **llama-4-maverick-17b-128e-instruct-fp8**.

  ![Adjust LLM settings](images/nav_43.png)

60. Click **Edit data mapping**.

  ![Edit Mapping](images/nav_44.png)

61. Hover over to the **modified_document_content** row and Click the **{x}** icon present in that row.
62. From the left panel, select **Fetch text content from URL modified**, then click **file_content**.

  ![Selection](images/nav_45.png)

63. Hover over to the **original_document_content** Crow and Click the **{x}** icon present in that row.
64. From the left panel, select **Fetch text content from URL original**, then click **file_content**.

  ![Selection](images/nav_46.png)

65. Click the close button.

  ![Close](images/prompt_close.png)

66. Double click on the **Output** node.
67. Click on the **Add** button.

  ![Output Add button](images/output_add.png)

68. Select **String**

  ![Select String](images/data_type.png)

69. In the **Name** field, enter the following and click the **Add** button
  ```
  output
  ```
  ![Output Name](images/output_variable.png)

70. Click **Edit data mapping**.

  ![Edit Mapping](images/nav_47.png)

71. Hover over to the **output** row and Click the **{x}** icon present in that row.

  ![Output Mapping](images/output_mapping.png)

72. From the left panel, select **Generative prompt**, then click **value**.

  ![Generated Prompt Variable](images/Generated_prompt.png)

73. Click the close button.

  ![Output close button](images/output_close_button.png)

74. You have now completed the workflow. Click **Done** to close the flow.

  ![Done](images/nav_48.png)

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="update_agent_behavior">
<summary><h3>4.4 Update Agent Behavior</h3></summary>

Before testing the agent, complete the Behavior section. Scroll to **Behavior** or select the **Behavior** tab on the left.

Add the following instructions:

```
If the user asks they want to compare between documents
-> Invoke the `document comparison tool` 
This tool will return the comparison result between the documents, You will just need to display it back to the user without any modifications

Also ensure you display the output of the tool only once without any repetitions.
```

  ![Behavior](images/behavior.png)

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="test_agent">
<summary><h3>4.5 Test the Agent</h3></summary>


1. Test your agent by entering the following query in the chat:

  ```
  I want to compare my legal contract documents.
  ```

2. The agent will ask you to upload your original contract: [Master Services Agreement - ACME Corp. 462390.docx](<documents/Master Services Agreement - ACME Corp. 462390.docx>)

3. Next, it will ask you to upload your modified contract:
[Modification Master Services Agreement - ACME Corp. 462390.docx](<documents/Modification Master Services Agreement - ACME Corp. 462390.docx>)

**Estimated Time for Comparison Result : 1.5 - 2 minutes**

4. You will see messages indicating:

  **Extracting the content from the original and modified contract**, followed by
  **Comparing the document contents**.

  ![Messages](images/messages.png)

5. The results should look similar to the image below:

> TODO update the result snapshot 

  ![Result](images/result.png)

[← Back to Table of contents](#table-of-contents)
</details>

<details open id="deploy_agent">
<summary><h3>4.6 Deploy the Agent (Optional)</h3></summary>

In this section, we will deploy the Legal Contract Comparison Agent along with the tool and workflow created earlier. Deployment ensures that the agents are accessible through watsonx Orchestrate chat and ready to handle real-time queries.

To deploy the Legal Contract Comparison Agent 

1. Turn on the toggle button for Home page so that your agent shows up in the watsonx Orchestrate Chat home page, once deployed.

  ![Toggle button](images/toggle_button.png)

2. Click the **Deploy** button in the top-right corner to deploy your agent.

  ![Deploy](images/deploy_button.png)

3. Click the **Deploy** button in the bottom-right corner of Pre-deployment summary page.

  ![Confirm Deploy](images/confirm_deploy.png)

4. To test the agent from the AI Chat window, click on the hamburger menu in the top left corner and then click on Chat.

  ![AI Chat](images/ai_chat.png)

5. Make sure your Legal Contract Comparison Agent is selected in the dropdown. You can now test your agent.

  ![Agent Selection](images/agent_selection.png)

[← Back to Table of contents](#table-of-contents)
</details>

</details>

<details open id="summary">
<summary><h2>5. Summary</h2></summary>

In this lab we automated the process of comparing two versions of a legal contract and highlighting the differences between them. We built a custom agent in watsonx Orchestrate, added an OpenAPI-based tool, and created an agentic workflow that guides the user through uploading the original and modified documents. The workflow then extracts text from both files, retrieves the content through the custom tool, and feeds the results into a generative prompt that produces a structured comparison of additions, deletions, and modifications. This provides a clear, reliable summary of every change made between contract versions.

The workflow can be extended with additional steps, such as automatically notifying reviewers, generating a change-impact summary, or triggering downstream approval processes. Using an agentic workflow ensures the comparison is handled consistently every time, while still allowing the agent to involve the legal reviewer whenever intervention is needed.

Combining agentic workflows with tools and task-level actions gives the agent the flexibility to handle both simple and multi-step processes. Users can chat with the agent to perform individual tasks, or rely on the workflow to manage complex document review operations from start to finish.

[← Back to Table of contents](#table-of-contents) | [← Back to Main page](../README.md)
</details>
