# Document Comparison with watsonx Orchestrate AI Agent

![](documents/doc_compare.jpg)

Ever spent hours combing through two nearly identical contracts trying to find the one clause that changes everything?

In this hands-on bootcamp, you’ll learn how to let AI handle the heavy lifting. See how IBM’s watsonx Orchestrate AI Agent can streamline document comparison and turn a tedious manual task into a fast, reliable workflow.

## What You’ll Learn

In this session, you’ll:

* Learn to orchestrate workflows in watsonx Orchestrate using a custom AI agent and tool.
* Extract document differences by interacting with the agent.
* Explore options for incorporating additional pre-built agents.

## Prerequisites

* Access to the IBM watsonx environment

## Use Case: Contract Review Accelerator

Imagine you’re part of a legal team reviewing two versions of a vendor contract:

* Version A from last quarter
* Version B received today

Instead of manually checking each clause, your watsonx Orchestrate agent handles it for you:

1. Extracts document terms.
2. Applies semantic matching to highlight critical differences such as pricing, liability, and renewal terms.
3. Generates a summary report for immediate review.

Within minutes, you’ll know what changed, why it matters, and what to do next.


## watsonx Orchestrate

<details open id="Environment_setup">
<summary><h2>Environment setup</h2></summary>

To access the watsonx Orchestrate console, go to the [Resources list on the IBM Cloud homepage](https://cloud.ibm.com/resources).

![alt text](documents/image1.png)

Expand the **AI / Machine Learning** section and select the resource that has **watsonx Orchestrate** in the Product column, as shown above. Then click **Launch watsonx Orchestrate**.

![alt text](documents/image2.png)

This opens the watsonx Orchestrate console.

![alt text](documents/image3.png)

</details>

<details open id="UI_walkthrough">
<summary><h2>UI walkthrough</h2></summary>

> When opening the console for the first time, you may see a pop-up prompting you to create your first agent. Click **Skip for now**.

![alt text](documents/image4.png)

The console shows that no agents have been deployed yet. If you interact with watsonx Orchestrate at this point, not much will happen because the system has no agents available to process requests.

Go ahead and chat with watsonx Orchestrate to see how it responds.

</details>

<details open id="Create_an_agent">
<summary><h2>Create an agent</h2></summary>

You are now ready to build your first agent. In the watsonx Orchestrate console, click either **Create or Deploy** or **Create new agent**. Both options lead to the same page.

![alt text](documents/image6.png)

If you add your document as a knowledge base for the agent, it will be able to perform tasks such as summarization.

![alt text](documents/image13.png)

![alt text](documents/image14.png)

![alt text](documents/image15.png)

![alt text](documents/image16.png)

![alt text](documents/image17.png)

![alt text](documents/image5.png)

</details>

<details open id="The_Legal_Contract_Comparison_Agent">
<summary><h2>The Legal Contract Comparison Agent</h2></summary>

On the next screen, click **Create agent**.

![alt text](documents/image7.png)

You can choose to create the agent from scratch or from a template, and provide a name and description.

Start by entering the following:

* **Name:**

  ```
  Legal Contract Comparison Agent
  ```
* **Description:**

  ```
  This agent is used to compare the differences between the legal contract documents provided.
  ```

In AI agent design, descriptions are not only documentation. They are used by the system to decide which agent to route a request to, so this field is important.

After entering the required information, click **Create**.

<img width="600" alt="image" src="documents/image8.png">

On the next screen, you can configure additional details about your agent.

* Agents can work with **Knowledge**, a **Toolset** (which includes Tools and Agents), or both, to satisfy incoming requests.
* You can also choose the **AI model**, the **agent style**, and the **voice modality**.

You can configure all of these elements here.

* **Knowledge** represents information stored as embeddings in a Vector Store. When the agent receives a request, it can search the connected knowledge repository to find relevant information. You can upload documents or link to an existing repository. Once again, the description field helps the agent decide whether a knowledge search is relevant.

* The **Toolset** contains components the agent can delegate tasks to.

  * **Tools** are functions the agent can call, such as APIs or custom code, extending the agent’s capabilities beyond what the LLM knows.
  * **Agents** are other agents, either within watsonx Orchestrate or external (such as watsonx.ai agents), that can handle a request or parts of it.

* You can select the **Large Language Model** the agent uses and the **style**. For this agent, select **llama-3-405b-instruct** and keep the **Default** style.

![Agent Style and Model](documents/agent_style_model.png)

#### Adding an OpenAPI tool

Next, add the required tool for this agent. To add a tool:

1. Click **Manage agents** at the top.
  ![Manage Agents](documents/manage_agents.png)

2. Click **All tools** in the left panel, then click **Create tool**.
  ![All tools](documents/all_tools.png)

3. Select **Add from file or MCP server**.
  ![Add from file or MCP server](documents/add_file.png)

4. Click **Import from file**.
  ![Import from file](documents/image21.png)

5. Click **Drag and drop an OpenAPI file here or click to upload.**
  ![Drag](documents/image22.png")

6. Download the **OpenAPI tool file**: [read-url-openapi.json](read-url-openapi.json) and upload it.
  ![upload](documents/image23.png")

7. **Select the checkbox** next to the operation name and click **Done**.

<img width="800" alt="image" src="documents/image24.png">

</details>

#### Create Agentic Workflow

We will create an agentic workflow and import it as a tool to be used by the agent.

Let’s go ahead and create the workflow.

1. Click **Add agents** on the left, then click the **Legal Contract Comparison Agent** you created earlier.

  ![Legal Contract Comparison Agent.png](<documents/Legal Contract Comparison Agent.png>)

2. Scroll down to the **Toolset** tab and click **Add Tool**.

3. Select **Create an agentic workflow**.

   <img width="800" alt="image" src="documents/image10.png">

4. Click the pencil icon next to **Edit details**.

  ![alt text](documents/edit_details.png)

5. Provide a `Name` and `Description` for the workflow, then click **Save**.

   * Name:

     ```
     document comparison tool
     ```
   * Description:

     ```
     Compare between legal documents
     ```

  ![Workflow name](documents/workflow_name.png)

6. Click the **+** button to start adding steps.

  ![Add option](documents/add.png)

7. Select **User activity**.

  ![User activity](documents/user_activity.png)

8. Click **Add +**.

  ![Add option](documents/add_option.png)

9. From the **Display to user** tab, select **Message**.

  ![Message](documents/message.png)

10. Double-click the message and add the following text in the **Output message** field:

```
Upload the original contract
```

  ![Output M  essage](documents/outputmessage.png)

11. Click **+** again.

  ![Add button](documents/second_add.png)

12. From the **Collect from user** tab, select **File upload**.

  ![File upload](documents/og_fileupload.png)

13. Double-click **File upload**, hover over **File upload 1**, and click the pencil icon.

  ![Pencil Icon](documents/file_upload_pencil_icon.png)

14. Update the title to:

```
Upload the original Contract
```

Then click the checkmark.

  ![Update name](documents/update_file_upload.png)

15. Click **+**.

  ![alt text](documents/second_add_option.png)

16. From **Display to user**, select **Message**.

17. Double-click the message and enter:

```
Upload the modified contract
```

  ![Modified](documents/modiified_message.png)

18. Click **+**.

  ![Modified File Upload](documents/modified_file_upload_add.png)

19. From **Collect from user**, select **File upload**.

20. Double-click it, hover over **File upload 1**, and click the pencil icon.

21. Update the title to:

```
Upload the modified contract
```

  ![Modified File Upload](documents/modified_file_upload.png)

22. Click **+**.

  ![Add button](documents/add_for_extract_msg.png)

23. From **Display to user**, select **Message**.

24. Double-click the message and enter:

```
Extracting the content from the original and modified contract
```

  ![Extraction Notification](documents/extraction_message.png)

25. Outside the User Activity box, click **+**.

  ![Add outside user activity box](documents/add_outside_user_activity.png)

26. From **Create new**, select **Text extractor**.

  ![Text extractor](documents/text_extractor.png)

27. Double-click **Text extractor 1**, hover over it, and click the pencil icon.

  ![Text Extractor](documents/text_extraction_pencil.png)

28. Update the title to:

```
Text extractor original
```

  ![Rename](documents/Rename_text_extractor.png)

29. Click **Edit data mapping**.

  ![Data Mapping](documents/edit_data_mapping.png)

30. Click the **{x}** icon.

  ![Variable](documents/variable.png)

31. From the left panel, select **Upload the original contract**.

  ![Original Contract](documents/og_contract.png)

32. Click **value**.

  ![Value](documents/value.png)

33. Close the dialog.

  ![Close](documents/close_button.png)

34. Click **+**.

  ![Add](documents/add_icon_.png)

35. Open the **Tools** tab and click the **+** icon next to **Fetch text content from URL**.

  ![Add tool](documents/fetch_text_from_urls.png)

36. Double-click **Fetch text content from URL**, hover over it, and click the pencil icon.

37. Update the title to:

```
Fetch text content from URL original
```

  ![Rename](documents/rename_tool.png)

38. Click **Edit data mapping**.

  ![mapping](documents/mapping.png)

39. Click the **{x}** icon.

  ![Mapping](documents/mapping2.png)

40. From the left, select **Text extractor original**, then select **output_file_ref**.

  ![Output file ref](documents/output_file_ref.png)

41. Click the close button.

  ![Close](documents/close2.png)

42. Click **+** again and, from the **Create new** tab, select **Text extractor**.

43. Double-click **Text extractor 2**, hover over it, and click the pencil icon.

44. Update the title to:

```
Text extractor modified
```

  ![Text extractor Modified](documents/Modified_text_extractor.png)

45. Click **Edit data mapping**.

46. Click the **{x}** icon.

47. From the left panel, select **Upload the modified contract**, then click **value**.

  ![value](documents/value2.png)

48. Click the close button.

  ![close](documents/close.png)

49. Click **+**.

50. Open the **Tools** tab and click the **+** icon next to **Fetch text content from URL**.

51. Double-click **Fetch text content from URL**, hover over it, and click the pencil icon.

52. Update the title to:

```
Fetch text content from URL modified
```

  ![rename](documents/tool_rename2.png)

53. Click **Edit data mapping**.

54. Click the **{x}** icon.

55. From the left, select **Text extractor modified**, then select **output_file_ref**.

  ![variable](documents/variable2.png)

56. Click the close button.

57. Click **+**.

58. Select **User activity**.

59. Click **Add +**.

60. From the **Display to user** tab, select **Message**.

61. Double-click the message and enter the following in **Output message**:

```
Comparing the document contents
```

  ![Compare message](documents/compare_message.png)

62. Outside the User Activity box, click **+**.

  ![Add Icon](documents/add_icon_for_prompt.png)

63. From the **Create new** tab, select **Generative prompt**.

  ![Generative Prompt](documents/prompt.png)

64. Click the pencil icon next to **Prompt Settings**.

  ![Prompt Settings](documents/prompt_settings.png)

65. Under **Define Prompts**, click **Add**.

  ![Define Prompts](documents/define_prompts.png)

66. Select **String**.

  ![string](documents/strings.png)

67. Under **Name**, enter:

```
original_document_content
```

68. Click **Add**.

  ![Orginal Document Content](documents/og_doc_content.png)

69. Add another input with the following name:

```
modified_document_content
```

! [Modified Document Content](documents/modified_doc_content.png)

70. For the **system prompt**, enter the following:

```
You are an expert Legal Contract Document Comparison Agent.
You will be provided with two legal contract documents:

- Original Document
- Modified Document

Your task is to perform a line-by-line comparison to identify all changes made in the Modified Document compared to the Original Document.

Requirements for your output:

Clearly highlight differences, including additions, deletions, and modifications of any sections.

Output format: The output should be well structured in the below format:

1. (Title of the difference)
    - Specify the section under which there is a difference
    - Original Text
    - Modified Text
    - Nature of Change (Added / Removed / Altered)

and so on for all differences.

DOs
- The response should directly begin with the formatted output structure specified above and nothing else.

DON’Ts
- DO NOT include unrelated commentary. Focus strictly on the differences.
- DO NOT repeat differences if they appear in multiple places.
```
67. For the **user prompt**, enter the following:

```
Here are the original and modified versions of the same document that I want you to compare.

1. Original Document content: {self.input.original_document_content}

2. Modified Document content: {self.input.modified_document_content}
```

  ![Prompts](documents/prompts.png)

68. Click **Adjust LLM settings** and set **New tokens** to **2000**.
69. Enable **Manually set the creative threshold settings**.

  ![Adjust LLM settings](documents/adjust_llm.png)

70. Set **Temperature** to **0.1**, **Top K** to **5**, and **Top P** to **0.95**.
71. Select the model **llama-3-405b-instruct**.

  ![LLM Settings](documents/llm_settings2.png)

72. Click **Edit data mapping**.

  ![Edit Mapping](documents/edit_map.png)

73. Click the **{x}** icon next to **modified_document_content**.
74. From the left panel, select **Fetch text content from URL modified**, then click **file_content**.

  ![Selection](documents/selection.png)

75. Click the **{x}** icon next to **original_document_content**.
76. From the left panel, select **Fetch text content from URL original**, then click **file_content**.

  ![Selection](documents/selection2.png)

77. Click the close button.

  ![Close](documents/prompt_close.png)

78. You have now completed the workflow. Click **Done** to close the flow.

  ![Done](documents/done.png)

---

### Update Agent Behavior

Before testing the agent, complete the Behavior section. Scroll to **Behavior** or select the **Behavior** tab on the left.

Add the following instructions:

```
If the user asks to compare documents
-> Invoke the `document_comparison_tool`
Display the output response of the tool back to the user
```

  ![Behavior](documents/behavior.png)

---

### Test the agent

1. Test your agent by entering the following query in the chat:

  ```
  I want to compare two document
  ```

2. The agent will ask you to upload your original contract. Upload [This Document](<Master Services Agreement - ACME Corp. 462390.docx>)

3. Next, it will ask you to upload your modified contract:
[Modified Document](<Modification Master Services Agreement - ACME Corp. 462390.docx>)

4. You will see messages indicating:

  **Extracting the content from the original and modified contract**, followed by
  **Comparing the document contents**.
  ![Messages](documents/messages.png)
5. The results should look similar to the image below:
  ![Result](documents/result.png)

</details>

### Deploy the agent

In this section, we will deploy the Legal Contract Comparison Agent along with the tool and workflow created earlier. Deployment ensures that the agents are accessible through watsonx Orchestrate chat and ready to handle real-time queries.

To deploy the Legal Contract Comparison Agent 

1. Turn on the toggle button for Home page so that your agent shows up in the watsonx Orchestrate Chat home page, once deployed.

  ![Toggle button](documents/toggle_button.png)
2. Click the **Deploy** button in the top-right corner to deploy your agent.

  ![Deploy](documents/deploy_button.png)
3. Click the **Deploy** button in the bottom-right corner of Pre-deployment summary page.

  ![Confirm Deploy](documents/confirm_deploy.png)
4. To test the Agent from the AI Chat window, click on the hamburger menu in the top left corner and then click on Chat.

  ![AI Chat](documents/ai_chat.png)

5. Make sure your Legal Contract Comparison Agent is selected in the dropdown. You can now test your agent.

  ![Agent Selection](documents/agent_selection.png)

<details open id="Summary">
<summary><h2>Summary</h2></summary>

In this part of the lab we automated the process of comparing two versions of a legal contract and highlighting the differences between them. We built a custom agent in watsonx Orchestrate, added an OpenAPI-based tool, and created an agentic workflow that guides the user through uploading the original and modified documents. The workflow then extracts text from both files, retrieves the content through the custom tool, and feeds the results into a generative prompt that produces a structured comparison of additions, deletions, and modifications. This provides a clear, reliable summary of every change made between contract versions.

The workflow can be extended with additional steps, such as automatically notifying reviewers, generating a change-impact summary, or triggering downstream approval processes. Using an agentic workflow ensures the comparison is handled consistently every time, while still allowing the agent to involve the legal reviewer whenever intervention is needed.

Combining agentic workflows with tools and task-level actions gives the agent the flexibility to handle both simple and multi-step processes. Users can chat with the agent to perform individual tasks, or rely on the workflow to manage complex document review operations from start to finish.
</details>

<details open id="Credits">
<summary><h2>Credits</h2></summary>

<details><summary>IBM Client Engineering Team</summary>

#### Business Technical Leader 
* Vincent Lee

#### Instructors
* Zack Phillips
* Pengxiang Xu
* Kyle Skyllingstad
* Chaithra M. Nagaraj
* Vrisan Dubey

#### AI Engineers
* M N Navneeth
* Tiyasa Mukherjee
* Fidha Haneefa
* Kousalya V

#### Designer
* Amy Luo

</details>

<details><summary> IBM Brand Team </summary>

#### Brand Technical Specialist
* Bill Tice
* Jishnu Desai

#### Brand Sales Specialist
* Pete Ingrasci

#### Account Technical Leader
* Effron Esseiva
  
</details>
